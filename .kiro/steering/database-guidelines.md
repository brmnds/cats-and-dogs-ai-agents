# Database Guidelines

_Amazon Aurora PostgreSQL - Pet Image AI Application_

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

## Database Choice: Amazon Aurora PostgreSQL

### Selected for Pet Image AI Application

**Amazon Aurora PostgreSQL** has been selected for the following reasons:

- **Managed Service**: Fully managed by AWS with automatic backups and scaling
- **High Availability**: Multi-AZ deployment with automatic failover
- **Performance**: Optimized for cloud with up to 3x performance of standard PostgreSQL
- **Integration**: Native integration with AWS Amplify and other AWS services
- **Cost-Effective**: Pay-per-use pricing suitable for 200-1K user scale
- **Security**: Built-in encryption, VPC isolation, and IAM integration

### Pet Image AI Schema

**Classification Records Table:**

```sql
CREATE TABLE classification_records (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_name VARCHAR(255) NOT NULL,
    image_url TEXT NOT NULL,
    classification VARCHAR(10) NOT NULL CHECK (classification IN ('cat', 'dog')),
    confidence DECIMAL(5,4) NOT NULL CHECK (confidence >= 0 AND confidence <= 1),
    processing_time INTEGER NOT NULL, -- milliseconds
    timestamp TIMESTAMP WITH TIME ZONE NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- Indexes for common queries
CREATE INDEX idx_classification_records_user_name ON classification_records(user_name);
CREATE INDEX idx_classification_records_timestamp ON classification_records(timestamp DESC);
CREATE INDEX idx_classification_records_classification ON classification_records(classification);
```

## Database Integration Guidelines

### AWS SDK and Native PostgreSQL Client

**For Pet Image AI Application:**

- Use AWS SDK for RDS connection management
- Native PostgreSQL client (pg) for type-safe queries
- Connection pooling through AWS RDS Proxy (optional)
- Environment-based configuration for different stages

**Connection Configuration:**

```typescript
interface DatabaseConfig {
  host: string;
  port: number;
  database: string;
  username: string;
  password: string;
  ssl: boolean;
}

// Example connection setup
const dbConfig: DatabaseConfig = {
  host: process.env.DATABASE_HOST!,
  port: parseInt(process.env.DATABASE_PORT!),
  database: process.env.DATABASE_NAME!,
  username: process.env.DATABASE_USERNAME!,
  password: process.env.DATABASE_PASSWORD!,
  ssl: true,
};
```

### General Principles

- Use TypeScript interfaces for all database models
- Implement proper error handling with graceful degradation
- Use parameterized queries to prevent SQL injection
- Handle connection errors without breaking classification functionality

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

### Pet Image AI Specific Guidelines

**Data Storage Requirements:**

- Store user name, classification result, confidence score, and timestamp
- Handle database unavailability gracefully (classification still works)
- Validate user input before database operations
- Log database errors for monitoring

**Error Handling Strategy:**

- Classification API should work even if database is down
- Display warning to user if data storage fails
- Retry database operations with exponential backoff
- Never block classification functionality due to database issues

**Performance Considerations:**

- Use connection pooling for concurrent requests
- Index on user_name and timestamp for common queries
- Monitor query performance and optimize as needed
- Consider read replicas for analytics queries (future)

---

_Note: This document is configured specifically for the Pet Image AI application using Amazon Aurora PostgreSQL._
