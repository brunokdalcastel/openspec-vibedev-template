# Authentication and Security Specification

## CRITICAL PREAMBLE
This spec exists because the developer is NOT a security specialist.
These rules are NON-NEGOTIABLE. The AI MUST follow them even when not asked.
Security shortcuts "for testing" or "to save time" are FORBIDDEN.

---

## Requirement: Authentication
The system SHALL use proven auth libraries only.

### Scenario: Auth implementation
- GIVEN a need for user auth
- WHEN implemented
- THEN a battle-tested library is used (NextAuth, Supabase Auth, Auth0, Clerk, Lucia, etc.)
- AND custom auth code is FORBIDDEN
- AND passwords hashed with bcrypt (cost 12+) or argon2
- AND session tokens are cryptographically random (min 256 bits)

### Scenario: Login
- GIVEN a login attempt
- WHEN credentials submitted
- THEN timing-safe comparison used
- AND failed response does NOT reveal if email or password was wrong
- AND lockout after 5 failures (exponential backoff)
- AND session ID regenerated on success (prevent fixation)

### Scenario: Sessions
- GIVEN an authenticated session
- WHEN managed
- THEN cookies: httpOnly + Secure + SameSite=Lax (or Strict)
- AND expiration defined (max 24h for sensitive apps)
- AND idle timeout invalidates session
- AND logout invalidates server-side (not just client cookie)

### Scenario: Passwords
- GIVEN password creation/change
- WHEN validated
- THEN min 8 chars, no max limit
- AND checked against breached databases (HaveIBeenPwned)
- AND common passwords rejected

## Requirement: Authorization
The system SHALL check permissions at every access point.

### Scenario: Resource access
- GIVEN authenticated user requesting a resource
- WHEN processed
- THEN server verifies user owns or has permission
- AND server-side only (never trust client)
- AND user A cannot access user B data (horizontal)
- AND regular user cannot access admin (vertical)

### Scenario: Roles
- GIVEN different user roles
- WHEN implemented
- THEN stored and verified server-side per request
- AND role changes effective immediately
- AND admin routes in separate group with middleware

## Requirement: Security Headers
The system SHALL include headers in all responses.

### Scenario: Headers
- GIVEN any HTTP response
- WHEN sent
- THEN includes:
  - `Content-Security-Policy` (restrictive)
  - `Strict-Transport-Security` (max-age=31536000; includeSubDomains)
  - `X-Content-Type-Options: nosniff`
  - `X-Frame-Options: DENY`
  - `Referrer-Policy: strict-origin-when-cross-origin`
  - `Permissions-Policy` (restrict camera, mic, geolocation)
- AND implemented via middleware (Helmet.js or equivalent)

## Requirement: Dependency Security
The system SHALL keep dependencies secure.

### Scenario: Audit
- GIVEN project dependencies
- WHEN managed
- THEN `npm audit` or equivalent in CI
- AND critical vulns block deployment
- AND Dependabot/Renovate configured
- AND lock files committed

### Scenario: Supply chain
- GIVEN new third-party package
- WHEN added
- THEN evaluated: maintenance, downloads, known issues
- AND permissions/scope reviewed
- AND version pinned

## Requirement: LGPD Compliance
The system SHALL comply with Brazilian data protection law.

### Scenario: Personal data
- GIVEN collection of personal data
- WHEN collected
- THEN explicit consent with clear purpose
- AND data minimization (only what's needed)
- AND users can export and delete their data
- AND processing purposes documented

## Requirement: File Uploads
The system SHALL handle uploads securely.

### Scenario: Upload processing
- GIVEN a file upload
- WHEN received
- THEN type validated by magic bytes (not just extension)
- AND size limited server-side
- AND filename sanitized (no path traversal)
- AND stored outside web root
- AND NEVER executed
