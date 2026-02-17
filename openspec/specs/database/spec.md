# Database Specification

## Requirement: Schema Management
The system SHALL use versioned migrations.

### Scenario: Schema change
- GIVEN a DB schema modification
- WHEN implemented
- THEN done via migration file (Prisma, Alembic, etc.)
- AND migration is reversible
- AND tested in staging before production
- AND destructive changes require explicit confirmation

### Scenario: Schema design
- GIVEN a new data model
- WHEN designed
- THEN indexes created for query patterns
- AND foreign keys enforce referential integrity
- AND NOT NULL where applicable
- AND soft delete preferred for user data

## Requirement: Query Security
The system SHALL prevent SQL injection.

### Scenario: Data access
- GIVEN any database query
- WHEN executed
- THEN uses ORM or parameterized statements
- AND string concatenation NEVER used
- AND user input NEVER interpolated into queries

### Scenario: Query logging
- GIVEN DB queries in dev/staging
- WHEN logged
- THEN sensitive values masked
- AND verbose query logging DISABLED in production

## Requirement: Data Protection
The system SHALL protect data at rest.

### Scenario: PII storage
- GIVEN personally identifiable information
- WHEN stored
- THEN passwords hashed (bcrypt cost 12+ or argon2)
- AND sensitive fields encrypted at rest where needed
- AND retention policies defined
- AND export/deletion available per user request (LGPD)

### Scenario: Backups
- GIVEN production database
- WHEN backup strategy defined
- THEN automated daily backups
- AND backups encrypted
- AND recovery tested periodically

## Requirement: Connection Security
The system SHALL secure DB connections.

### Scenario: Connection config
- GIVEN app connecting to DB
- WHEN connection established
- THEN connection string from env var (never hardcoded)
- AND SSL/TLS enforced for remote
- AND connection pooling configured
- AND DB user has minimum required privileges (not root)

## Requirement: Performance
The system SHALL maintain query performance.

### Scenario: Query optimization
- GIVEN queries serving users
- WHEN written
- THEN N+1 avoided (eager loading/joins)
- AND indexes on WHERE/ORDER BY/JOIN columns
- AND EXPLAIN used for complex queries
