# Code Quality Check Hook

*Lightweight pre-commit validation for maintaining code quality*

## Purpose
This hook provides minimal quality gates to catch common issues before code is committed, ensuring consistent code quality across the project.

## Validation Steps

### 1. TypeScript Type Checking
```bash
tsc --noEmit
```
- Validates TypeScript types across the entire project
- Catches type errors before they reach production
- Ensures type safety is maintained

### 2. ESLint Code Linting
```bash
eslint . --ext .ts,.tsx,.js,.jsx
```
- Enforces code style and best practices
- Catches potential bugs and code smells
- Maintains consistent coding patterns

### 3. Prettier Code Formatting
```bash
prettier --check .
```
- Ensures consistent code formatting
- Maintains readable and professional code style
- Reduces formatting-related code review discussions

### 4. Build Verification
```bash
npm run build
```
- Verifies that the project builds successfully
- Catches build-time errors early
- Ensures deployability of the code

## Implementation Options

### Option 1: Pre-commit Hook (Recommended)
Install and configure using husky and lint-staged:

```bash
npm install --save-dev husky lint-staged
```

Add to package.json:
```json
{
  "lint-staged": {
    "*.{ts,tsx,js,jsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  },
  "scripts": {
    "prepare": "husky install"
  }
}
```

### Option 2: GitHub Action
Create `.github/workflows/code-quality.yml`:
```yaml
name: Code Quality Check
on: [push, pull_request]
jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '22'
      - run: npm ci
      - run: tsc --noEmit
      - run: eslint . --ext .ts,.tsx,.js,.jsx
      - run: prettier --check .
      - run: npm run build
```

### Option 3: Manual Script
Add to package.json scripts:
```json
{
  "scripts": {
    "quality-check": "tsc --noEmit && eslint . --ext .ts,.tsx,.js,.jsx && prettier --check . && npm run build"
  }
}
```

## Configuration Files

### ESLint Configuration (.eslintrc.js)
```javascript
module.exports = {
  extends: [
    'eslint:recommended',
    '@typescript-eslint/recommended',
    'next/core-web-vitals'
  ],
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  rules: {
    // Add project-specific rules here
  }
};
```

### Prettier Configuration (.prettierrc)
```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2
}
```

### TypeScript Configuration (tsconfig.json)
```json
{
  "compilerOptions": {
    "strict": true,
    "noEmit": true,
    "target": "es2022",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve",
    "incremental": true
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}
```

## Expansion Opportunities

As the project matures, consider adding:

### Additional Checks
- **Unit Test Execution**: Run tests before commit
- **Security Scanning**: Check for known vulnerabilities
- **Bundle Size Analysis**: Monitor bundle size changes
- **Performance Audits**: Lighthouse CI for performance regression
- **Dependency Audits**: Check for outdated or vulnerable dependencies

### Advanced Linting
- **Import Sorting**: Consistent import organization
- **Unused Code Detection**: Find and remove dead code
- **Complexity Analysis**: Monitor code complexity metrics
- **Documentation Linting**: Ensure proper JSDoc comments

### Integration Tests
- **API Endpoint Testing**: Validate API contracts
- **Database Migration Testing**: Ensure migrations work correctly
- **End-to-End Testing**: Critical user journey validation

## Troubleshooting

### Common Issues
- **Slow Hook Execution**: Consider running checks only on staged files
- **False Positives**: Adjust ESLint rules for project needs
- **Build Failures**: Ensure all dependencies are properly installed
- **Type Errors**: Keep TypeScript configuration up to date

### Performance Optimization
- Use `lint-staged` to run checks only on changed files
- Cache TypeScript compilation results
- Run checks in parallel when possible
- Skip checks for certain file types or directories

---

*Note: Start with the basic validation steps and expand based on project needs and team preferences. The goal is to catch issues early without slowing down development velocity.*