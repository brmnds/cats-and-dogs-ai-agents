# Database Guidelines

_Draft framework - to be defined based on database choice and requirements_

## Database Operations & Safety

### Critical Safety Principles

**NEVER perform destructive operations without explicit confirmation:**

- ❌ Do NOT delete databases, tables, or production data without consulting first
- ❌ Do NOT drop schemas, truncate tables, or perform bulk deletions
- ❌ Do NOT remove indexes or constraints without understanding impact
- ✅ ALWAYS ask for explicit confirmation before any irreversible action
- ✅ When in doubt about data safety, ask for clarification and double-check

### Data Management Practices

**Schema Design:**

- Use consistent naming conventions (snake_case for tables/columns)
- Implement proper foreign key relationships
- Add appropriate indexes for query performance
- Include created_at and updated_at timestamps where relevant

**Migration Strategy:**

- All schema changes through versioned migrations
- Test migrations on development data first
- Backup production data before major migrations
- Rollback procedures for failed migrations

**Query Optimization:**

- Use appropriate indexes for common queries
- Monitor slow query logs
- Optimize N+1 query problems
- Use connection pooling for better performance

## Development Workflow

### Local Development

- Use consistent database setup across team
- Seed data for development and testing
- Environment-specific configuration
- Docker containers for database consistency (optional)

### Data Validation

- Implement validation at application level
- Use database constraints for data integrity
- Proper error handling for constraint violations
- Input sanitization to prevent injection attacks

### Backup & Recovery

- Regular automated backups
- Test backup restoration procedures
- Point-in-time recovery capabilities
- Document recovery procedures

## Database Choice Considerations

### For 200-1K Users Scale

**SQLite:**

- Pros: Simple setup, no server required, excellent for development
- Cons: Limited concurrent writes, not suitable for distributed systems
- Best for: Single-server applications, development, small scale

**PostgreSQL:**

- Pros: Feature-rich, excellent JSON support, strong consistency
- Cons: More complex setup, higher resource usage
- Best for: Complex queries, JSON data, future scalability

**MySQL:**

- Pros: Mature, well-documented, good performance
- Cons: Less advanced features than PostgreSQL
- Best for: Traditional relational data, proven reliability

## ORM/Query Builder Guidelines

### General Principles

- Use TypeScript-first solutions when possible
- Prefer type-safe query builders
- Implement proper error handling
- Use transactions for multi-step operations

### Migration Management

- Version control all migration files
- Never edit existing migrations
- Use descriptive migration names
- Test migrations in development first

### Performance Considerations

- Use select only needed columns
- Implement proper pagination
- Cache frequently accessed data
- Monitor query performance

## Security Guidelines

### Access Control

- Use least privilege principle for database users
- Separate read/write permissions where appropriate
- Environment-specific database credentials
- Regular credential rotation

### Data Protection

- Encrypt sensitive data at rest
- Use parameterized queries to prevent SQL injection
- Implement proper input validation
- Audit sensitive data access

---

_Note: This document will be expanded once the database technology is chosen and specific requirements are defined._
