# Backend Specification

## Requirement: Endpoint Standards
The system SHALL enforce secure, consistent endpoints.

### Scenario: New endpoint
- GIVEN a new API endpoint
- WHEN implemented
- THEN includes: input validation, auth check, authz check, rate limit, error handling
- AND returns appropriate HTTP status codes
- AND uses typed request/response schemas

### Scenario: Error responses
- GIVEN an error during processing
- WHEN error is returned to client
- THEN internal details (stack traces, SQL, file paths) are NEVER exposed
- AND response uses consistent format: `{error, code}`
- AND full error is logged server-side for debugging

## Requirement: Input Validation
The system SHALL validate ALL input at every boundary.

### Scenario: Request body
- GIVEN an endpoint receiving JSON
- WHEN processed
- THEN body validated against strict schema
- AND unexpected fields stripped (no mass assignment)
- AND validation errors return 400 with field-specific messages

### Scenario: URL params and query strings
- GIVEN path params or query strings
- WHEN processed
- THEN validated for type, format, and range
- AND excessively long values rejected

## Requirement: Service Layer
The system SHALL separate business logic from transport.

### Scenario: Business logic
- GIVEN feature logic
- WHEN implemented
- THEN resides in service/use-case layer (not route handlers)
- AND testable independently of HTTP framework
- AND has typed inputs and outputs

## Requirement: Logging
The system SHALL log structured data.

### Scenario: Request logging
- GIVEN any API request
- WHEN processed
- THEN method, path, status, duration logged
- AND sensitive data (passwords, tokens, PII) NEVER logged
- AND each request has correlation ID

## Requirement: Configuration
The system SHALL manage config securely.

### Scenario: Env vars
- GIVEN application config
- WHEN app starts
- THEN all required vars validated at startup (fail fast)
- AND .env in .gitignore
- AND no default values for secrets
