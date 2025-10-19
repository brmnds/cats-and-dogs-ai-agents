# Project Infrastructure Documentation

_This document provides an overview of the project's technical architecture and serves as context for AI assistants and developers working on the project._

## Project Overview

### Purpose

[TO BE DEFINED] - Brief description of what the application does and its primary purpose.

### Target User Base

- **Scale**: 200-1,000 users
- **User Types**: [TO BE DEFINED] - Define primary user personas and their needs
- **Growth Expectations**: [TO BE DEFINED] - Expected growth trajectory and scaling considerations

## Repository Structure

This project uses a monorepo structure organized as follows:

### `/apps/`

Contains the main applications:

- **Purpose**: Frontend applications and user-facing services
- **Examples**: Web app (Next.js), admin dashboard, mobile app
- **Structure**: Each app is self-contained with its own package.json

### `/services/`

Contains backend services and APIs:

- **Purpose**: Backend services, APIs, and microservices
- **Examples**: Main API, authentication service, notification service
- **Structure**: Independently deployable services with their own package.json

### `/packages/`

Contains shared packages and libraries:

- **Purpose**: Reusable code shared across apps and services
- **Examples**: UI components, utilities, types, database schema
- **Structure**: Publishable packages with their own package.json

### `/infra/`

Contains infrastructure as code:

- **Purpose**: Deployment configurations and infrastructure management
- **Examples**: Terraform, Docker, Kubernetes, deployment scripts
- **Structure**: Environment-specific configurations and IaC files

### `/docs/`

Contains project documentation:

- **Purpose**: Technical documentation, API docs, guides
- **Examples**: Architecture docs, API documentation, user guides
- **Structure**: Organized by topic and audience

### `/scripts/`

Contains utility scripts:

- **Purpose**: Development and operational scripts
- **Examples**: Setup, build, deployment, and maintenance scripts
- **Structure**: Executable scripts with clear documentation

## Steering Documents

The `.kiro/steering/` directory contains key guidelines:

### `engineering-principles.md`

- Core development philosophy for 200-1K user scale
- Code quality standards and testing strategy
- Performance goals and security mindset
- Development workflow and best practices

### `technology-stack.md`

- Current stable versions (October 2025)
- Technology choices and decision criteria
- Framework and tool selections
- Infrastructure and deployment options

### `database-guidelines.md`

- Database operations and safety protocols
- Migration strategies and data management
- Performance optimization guidelines
- Security and backup procedures

### `ai-development-guide.md`

- AI model selection and prompt engineering
- Error handling and reliability patterns
- Context management and testing strategies
- Performance optimization for AI features

### `brand-design-system.md`

- Visual foundation and color system
- Typography and spacing standards
- Component guidelines and accessibility
- Design token implementation

## Architecture

### High-Level System Architecture

[TO BE DEFINED] - System architecture diagram and component relationships

### Key Technology Choices

Based on October 2025 stable versions:

- **Runtime**: Node.js v22.20.0 (LTS)
- **Frontend**: Next.js v15.5.6 with React
- **Language**: TypeScript with strict mode
- **Database**: [TO BE DEFINED] - PostgreSQL, MySQL, or SQLite
- **Deployment**: [TO BE DEFINED] - Vercel, AWS, or Railway

### Infrastructure Overview

[TO BE DEFINED] - Deployment architecture, hosting, and service dependencies

## Development

### Local Setup

```bash
# Clone the repository
git clone [REPOSITORY_URL]
cd [PROJECT_NAME]

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local with your configuration

# Start development
npm run dev
```

### Environment Configuration

Required environment variables in `.env.local`:

```bash
# Database
DATABASE_URL="[TO BE DEFINED]"

# Authentication
NEXTAUTH_SECRET="[TO BE DEFINED]"
NEXTAUTH_URL="http://localhost:3000"

# External Services
# [TO BE DEFINED based on integrations]
```

### Key Commands

```bash
# Development
npm run dev          # Start development server
npm run build        # Build for production
npm run start        # Start production server

# Quality Checks
npm run type-check   # TypeScript type checking
npm run lint         # ESLint code linting
npm run format       # Prettier code formatting
npm run test         # Run test suite

# Database
npm run db:migrate   # Run database migrations
npm run db:seed      # Seed development data
npm run db:studio    # Open database studio
```

## Deployment

### Deployment Strategy

- **Current**: Direct to production deployment
- **Process**: Automated testing → Build → Deploy
- **Rollback**: [TO BE DEFINED] - Rollback procedures for critical issues

### Environment Variables Management

- **Development**: `.env.local` file (not committed)
- **Production**: Platform-specific environment variable management
- **Secrets**: Secure secret management (never commit secrets)

### Deployment Platforms

[TO BE DEFINED] - Specific deployment configuration based on chosen platform:

- Vercel for Next.js applications
- AWS for full-stack applications
- Railway for simple deployments

## Safety Principles

### Critical Safety Guidelines

**NEVER perform destructive operations without explicit confirmation:**

- ❌ Do NOT delete databases, tables, or production data
- ❌ Do NOT drop schemas, truncate tables, or perform bulk deletions
- ❌ Do NOT remove IAM roles, security groups, or production infrastructure
- ✅ ALWAYS ask for explicit confirmation before any irreversible action
- ✅ When in doubt about data safety, ask for clarification

### Destructive Operation Protocols

1. **Identify the operation** - Clearly state what will be affected
2. **Assess the impact** - Understand the scope and consequences
3. **Request confirmation** - Get explicit approval from authorized personnel
4. **Document the action** - Log what was done and why
5. **Verify the result** - Confirm the operation completed as expected

### High-Risk Operations

- Database operations (drops, truncates, bulk deletes)
- Infrastructure changes (resource deletion, security modifications)
- Production deployments with breaking changes
- User data modifications or deletions
- Security configuration changes

## Monitoring & Maintenance

### Performance Monitoring

[TO BE DEFINED] - Monitoring strategy and key metrics

### Error Tracking

[TO BE DEFINED] - Error tracking and alerting setup

### Backup & Recovery

[TO BE DEFINED] - Backup procedures and disaster recovery plans

---

_Note: This document serves as a living guide and should be updated as the project architecture evolves. Sections marked [TO BE DEFINED] should be filled in as architectural decisions are made._
