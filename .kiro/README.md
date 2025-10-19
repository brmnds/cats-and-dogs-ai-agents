# Kiro Configuration

This directory contains Kiro-specific configuration and documentation for the project.

## Directory Structure

### `/steering/`

Contains steering documents that provide context and guidelines for AI-assisted development:

- `engineering-principles.md` - Core development philosophy and standards
- `technology-stack.md` - Technology choices and decision criteria
- `database-guidelines.md` - Database operations and safety guidelines
- `ai-development-guide.md` - AI development best practices
- `brand-design-system.md` - Design system and brand guidelines

### `/hooks/`

Contains agent hooks for automated development workflows:

- `code-quality-check.md` - Pre-commit quality validation

### `/specs/`

Contains feature specifications created through Kiro's spec workflow:

- Each feature has its own directory with requirements, design, and tasks

### `/settings/`

Contains Kiro configuration files:

- `mcp.json` - Model Context Protocol server configuration

## Usage

### Steering Documents

These documents are automatically included as context when working with Kiro. They help ensure consistent development practices and decision-making across the project.

### Specs Workflow

Use Kiro's spec workflow to:

1. Define feature requirements
2. Create technical designs
3. Generate implementation task lists
4. Execute tasks systematically

### Hooks

Agent hooks can be triggered automatically or manually to maintain code quality and automate repetitive tasks.

## Customization

All documents in this directory are designed to be customized for your specific project needs. Start with the provided frameworks and refine them based on your team's preferences and project requirements.
