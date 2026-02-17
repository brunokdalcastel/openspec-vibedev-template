# API Specification

## Requirement: RESTful Design
The system SHALL follow REST conventions.

### Scenario: Resource endpoints
- GIVEN a resource to expose
- WHEN endpoints are designed
- THEN follow REST (GET/POST/PUT/PATCH/DELETE)
- AND resource names are plural nouns (`/api/v1/users`)
- AND API is versioned (v1, v2)
- AND responses use consistent envelope: `{data, meta, error}`

### Scenario: Pagination
- GIVEN a list endpoint
- WHEN queried
- THEN pagination implemented (cursor or offset)
- AND default and max page size defined
- AND total count in meta when feasible

## Requirement: API Security
The system SHALL secure all endpoints.

### Scenario: Authentication
- GIVEN a protected endpoint
- WHEN request lacks valid auth
- THEN 401 returned
- AND no resource info leaked

### Scenario: Authorization
- GIVEN an authenticated user
- WHEN user lacks permission
- THEN 403 returned
- AND attempt logged
- AND object-level authz enforced (user A can't access user B data)

### Scenario: Rate limiting
- GIVEN any endpoint
- WHEN rate limit exceeded
- THEN 429 returned with Retry-After header
- AND rate limit headers included (X-RateLimit-*)

### Scenario: CORS
- GIVEN API serving a frontend
- WHEN CORS configured
- THEN origins explicitly listed (NEVER wildcard in production)
- AND methods restricted to what's needed

## Requirement: Documentation
The system SHALL maintain API docs.

### Scenario: OpenAPI spec
- GIVEN any endpoint
- WHEN created or modified
- THEN OpenAPI/Swagger updated
- AND request/response schemas documented
- AND examples provided

## Requirement: Webhooks (if applicable)
The system SHALL secure webhook endpoints.

### Scenario: Incoming webhooks
- GIVEN an external webhook endpoint
- WHEN request arrives
- THEN signature verified against shared secret
- AND payload validated
- AND replay prevented (timestamp check)
- AND processing is idempotent
