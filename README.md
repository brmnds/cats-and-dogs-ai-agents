# Kiro Project

A modern web application built with the Kiro development framework, designed for applications serving 200-1,000 users.

## Quick Start

```bash
# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local with your configuration

# Start development
npm run dev
```

## Project Structure

This is a monorepo containing:

- **`apps/`** - Frontend applications (Next.js web app, admin dashboard)
- **`services/`** - Backend services and APIs
- **`packages/`** - Shared libraries and components
- **`infra/`** - Infrastructure as code and deployment configs
- **`docs/`** - Project documentation

## Technology Stack

- **Runtime**: Node.js v22.20.0 (LTS)
- **Frontend**: Next.js v15.5.6 with React
- **Language**: TypeScript with strict mode
- **Monorepo**: Turborepo with npm workspaces
- **Code Quality**: ESLint, Prettier, Husky

## Development

### Available Scripts

```bash
npm run dev          # Start development servers
npm run build        # Build all packages and apps
npm run lint         # Lint all code
npm run format       # Format code with Prettier
npm run type-check   # TypeScript type checking
npm run test         # Run test suites
npm run quality-check # Run all quality checks
```

### Code Quality

This project uses automated code quality checks:

- Pre-commit hooks with Husky and lint-staged
- TypeScript strict mode for type safety
- ESLint for code linting
- Prettier for consistent formatting

## Documentation

For detailed technical documentation, architecture overview, and development guidelines, see [CLAUDE.md](./CLAUDE.md).

## Kiro Framework

This project uses the Kiro development framework with:

- **Steering documents** in `.kiro/steering/` for development guidelines
- **Spec workflow** in `.kiro/specs/` for feature development
- **Agent hooks** in `.kiro/hooks/` for automated workflows
- **MCP integration** for enhanced AI assistance

## Getting Help

- Check [CLAUDE.md](./CLAUDE.md) for technical architecture details
- Review steering documents in `.kiro/steering/` for development guidelines
- Use Kiro's spec workflow for new feature development

---

Built with ❤️ using the Kiro development framework
