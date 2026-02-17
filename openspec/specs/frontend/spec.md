# Frontend Specification

## Requirement: Component Architecture
The system SHALL use consistent component patterns.

### Scenario: Component creation
- GIVEN a new UI feature
- WHEN a component is created
- THEN it has typed props (TypeScript / PropTypes)
- AND handles loading, error, and empty states
- AND is responsive (mobile-first)

### Scenario: Form handling
- GIVEN a form collecting user input
- WHEN implemented
- THEN client-side validation mirrors server-side schema
- AND error messages are user-friendly (no technical details)
- AND submit is disabled during submission (no double-submit)
- AND CSRF protection is applied

## Requirement: Frontend Security
The system SHALL prevent client-side vulnerabilities.

### Scenario: Rendering user content
- GIVEN user-generated content to display
- WHEN rendered
- THEN sanitized against XSS (DOMPurify or framework auto-escaping)
- AND raw HTML injection NEVER used with user data
- AND CSP headers prevent inline script execution

### Scenario: Token storage
- GIVEN auth tokens in the frontend
- WHEN stored
- THEN httpOnly cookies are used (NEVER localStorage for auth)
- AND tokens are NEVER logged to console
- AND tokens are NEVER sent to third-party scripts

### Scenario: API calls
- GIVEN frontend calling backend APIs
- WHEN requests are made
- THEN auth via httpOnly cookies or Authorization header
- AND CORS rejects unknown origins
- AND errors shown to user are generic (no internal details)

## Requirement: Accessibility
The system SHALL be accessible.

### Scenario: Interactive elements
- GIVEN clickable/interactive elements
- WHEN implemented
- THEN ARIA labels are present
- AND keyboard navigation works
- AND focus states are visible
- AND color is not the only indicator

## Requirement: Performance
The system SHALL optimize load times.

### Scenario: Bundle
- GIVEN the production build
- WHEN built
- THEN code splitting applied per route
- AND images optimized (WebP, lazy load)
- AND unused dependencies removed
