# DeepLX Test Suite

This directory contains comprehensive tests for DeepLX. The test suite is designed to ensure reliability, performance, and security of the translation service.

## Test Structure

```
tests/
├── lib/                    # Unit tests for library modules
│   ├── query.test.ts      # Core translation functionality
│   ├── cache.test.ts      # Caching system tests
│   ├── rateLimit.test.ts  # Rate limiting tests
│   ├── proxyManager.test.ts # Proxy management tests
│   ├── circuitBreaker.test.ts # Circuit breaker tests
│   ├── retryLogic.test.ts # Retry mechanism tests
│   ├── security.test.ts   # Security middleware tests
│   ├── validation.test.ts # Input validation tests
│   ├── textUtils.test.ts  # Text processing utilities
│   ├── types.test.ts      # Type definitions and utilities
│   └── errorHandler.test.ts # Error handling tests
├── integration/           # Integration tests
│   └── translation.test.ts # End-to-end translation workflows
├── performance/           # Performance and load tests
│   └── load.test.ts      # Load testing and benchmarks
├── utils/                 # Test utilities and helpers
│   └── testHelpers.ts    # Common test utilities
├── setup.ts              # Jest setup configuration
└── README.md             # This file
```

## Test Categories

### Unit Tests (`tests/lib/`)

Unit tests focus on individual modules and functions in isolation:

- **Query Module**: Tests core translation functionality, request building, and API communication
- **Cache Module**: Tests translation caching, cache key generation, and cache invalidation
- **Rate Limiting**: Tests token bucket algorithm, IP-based limiting, and rate limit recovery
- **Proxy Management**: Tests proxy selection, and failover logic
- **Circuit Breaker**: Tests failure detection, circuit states, and recovery mechanisms
- **Retry Logic**: Tests exponential backoff, retry conditions, and failure handling
- **Security**: Tests input sanitization, CORS handling, and IP validation
- **Validation**: Tests request validation, parameter sanitization, and error reporting
- **Text Utils**: Tests text chunking, payload estimation, and length validation
- **Error Handling**: Tests error response formatting and error categorization

### Integration Tests (`tests/integration/`)

Integration tests verify complete workflows and component interactions:

- **End-to-end Translation**: Complete translation workflows with caching and rate limiting
- **Proxy Failover**: Proxy selection and automatic failover scenarios
- **Security Integration**: Input validation and sanitization in real workflows
- **Performance Integration**: Response time and resource utilization under load

### Performance Tests (`tests/performance/`)

Performance tests ensure the service meets performance requirements:

- **Response Time Benchmarks**: Measure translation response times
- **Memory Usage**: Monitor memory consumption and leak detection
- **Concurrent Requests**: Test handling of simultaneous requests
- **Load Testing**: Stress testing with high request volumes
- **Resource Utilization**: CPU and memory usage under various loads

## Running Tests

### All Tests

```bash
npm test
```

### Test Categories

```bash
# Unit tests only
npm run test:unit

# Integration tests only
npm run test:integration

# Performance tests only
npm run test:performance

# With coverage report
npm run test:coverage

# Continuous integration mode
npm run test:ci
```

### Development Mode

```bash
# Watch mode for development
npm run test:watch

# Verbose output for debugging
npm run test:verbose

# Debug mode with detailed output
npm run test:debug
```

## Test Configuration

### Jest Configuration (`jest.config.js`)

The test suite uses Jest with the following key configurations:

- **Environment**: Miniflare for Cloudflare Workers simulation
- **TypeScript**: ts-jest for TypeScript support
- **Coverage**: Comprehensive coverage reporting
- **Mocking**: Extensive mocking of external dependencies

### Environment Setup (`tests/setup.ts`)

Global test setup includes:

- Mock environment creation
- Global utilities and matchers
- Console output management
- Request/Response mocking

## Writing Tests

### Test Structure

Follow this structure for new tests:

```typescript
describe('Module Name', () => {
  let mockEnv: Env;

  beforeEach(() => {
    mockEnv = createMockEnv();
  });

  afterEach(() => {
    jest.clearAllMocks();
  });

  describe('function name', () => {
    it('should handle normal case', () => {
      // Test implementation
    });

    it('should handle error case', () => {
      // Error test implementation
    });
  });
});
```

### Best Practices

1. **Isolation**: Each test should be independent and not rely on other tests
2. **Mocking**: Mock external dependencies and focus on the unit under test
3. **Coverage**: Aim for high code coverage but focus on meaningful tests
4. **Error Cases**: Test both success and failure scenarios
5. **Edge Cases**: Include boundary conditions and edge cases
6. **Performance**: Include performance assertions where relevant

### Custom Matchers

The test suite includes custom Jest matchers:

```typescript
expect(response).toBeValidTranslationResponse();
expect(response).toBeValidErrorResponse();
```

### Test Utilities

Use the provided test utilities for common operations:

```typescript
import {
  createMockTranslationResponse,
  createMockErrorResponse,
  createTestEnvironment,
  expectValidTranslationResponse
} from './utils/testHelpers';
```

## Continuous Integration

The test suite runs automatically on:

- **Push to main/develop branches**
- **Pull requests to main branch**
- **Multiple Node.js versions** (18.x, 20.x)

### CI Pipeline

1. **Lint**: TypeScript type checking
2. **Unit Tests**: All library module tests
3. **Integration Tests**: End-to-end workflow tests
4. **Performance Tests**: Load and performance benchmarks
5. **Coverage**: Code coverage reporting

## Coverage Requirements

The test suite aims for:

- **Line Coverage**: > 90%
- **Function Coverage**: > 95%
- **Branch Coverage**: > 85%
- **Statement Coverage**: > 90%

## Debugging Tests

### Common Issues

1. **Async/Await**: Ensure all async operations are properly awaited
2. **Mocking**: Verify mocks are properly reset between tests
3. **Timeouts**: Increase timeout for slow operations
4. **Memory**: Clear references to prevent memory leaks

### Debug Commands

```bash
# Run specific test file
npm test -- query.test.ts

# Run with debug output
npm run test:debug

# Run single test
npm test -- --testNamePattern="should handle successful translation"
```

## Contributing

When adding new features:

1. **Write tests first** (TDD approach recommended)
2. **Update existing tests** if behavior changes
3. **Add integration tests** for new workflows
4. **Include performance tests** for performance-critical features
5. **Update documentation** including this README

## Monitoring and Alerts

The test suite includes monitoring for:

- **Test execution time trends**
- **Flaky test detection**
- **Coverage regression alerts**
- **Performance regression detection**

For questions or issues with the test suite, please refer to the main repository documentation or create an issue in the repository.
