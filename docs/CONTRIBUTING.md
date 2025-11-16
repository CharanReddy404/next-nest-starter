# Contributing Guide

Thank you for considering contributing to this project! This guide will help you get started.

## Development Setup

### Prerequisites
- Node.js 18+
- pnpm 10.0.0
- Git

### Initial Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/acttory.git
   cd acttory
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Install Biome VS Code Extension** (recommended)
   - Open VS Code
   - Install "Biome" extension (`biomejs.biome`)
   - Reload VS Code

4. **Verify setup**
   ```bash
   # Check types
   pnpm check-types

   # Lint code
   pnpm lint

   # Build all packages
   pnpm build
   ```

## Development Workflow

### Running Services

**Frontend:**
```bash
cd services/acttory-fe
pnpm dev
# Opens at http://localhost:3000
```

**Backend:**
```bash
cd services/acttory-be
pnpm start:dev
# Runs at http://localhost:3001
```

### Code Quality

Before committing, ensure:

1. **TypeScript compiles**
   ```bash
   pnpm check-types
   ```

2. **Code is linted**
   ```bash
   pnpm lint:fix
   ```

3. **Tests pass** (when implemented)
   ```bash
   pnpm test
   ```

### Git Workflow

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make changes**
   - Write code
   - Add tests (when test infrastructure is ready)
   - Update documentation if needed

3. **Commit changes**
   ```bash
   git add .
   git commit -m "feat: add awesome feature"
   ```

   Git hooks will automatically:
   - Run Biome linting
   - Format code
   - Organize imports

4. **Push and create PR**
   ```bash
   git push origin feature/your-feature-name
   ```

## Commit Convention

We follow [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `style:` - Code style changes (formatting, etc.)
- `refactor:` - Code refactoring
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks

**Examples:**
```bash
feat: add user authentication
fix: resolve login redirect issue
docs: update API documentation
refactor: improve error handling
test: add unit tests for user service
chore: update dependencies
```

## Code Style

### Biome Configuration

The project uses Biome for linting and formatting. Configuration is in `biome.json`.

**Key rules:**
- 2 space indentation
- Double quotes for strings
- Semicolons required
- 100 character line width
- No unused variables
- Prefer `const` over `let`

### TypeScript

- Use TypeScript strict mode
- Avoid `any` type (use `unknown` if needed)
- Define interfaces for all data structures
- Use type imports: `import type { User } from './types'`

### File Naming

- **Components:** PascalCase (`UserProfile.tsx`)
- **Utilities:** camelCase (`formatDate.ts`)
- **Types:** PascalCase (`User.ts`)
- **Config files:** lowercase with dashes (`biome.json`)

## Project Structure

### Adding a New Service

1. Create folder in `services/`
2. Add to `pnpm-workspace.yaml`
3. Create `package.json` with workspace dependencies
4. Add TypeScript config extending shared config
5. Update `turbo.json` if needed

### Adding a New Shared Package

1. Create folder in `packages/`
2. Add `package.json`:
   ```json
   {
     "name": "@acttory/package-name",
     "version": "0.0.0",
     "private": true,
     "main": "./dist/index.js",
     "types": "./dist/index.d.ts"
   }
   ```
3. Add `tsconfig.json`:
   ```json
   {
     "extends": "@acttory/tsconfig/library.json"
   }
   ```
4. Create `src/index.ts`
5. Add to consuming packages:
   ```bash
   pnpm add @acttory/package-name@workspace:*
   ```

## Testing Guidelines (Future)

### Unit Tests
- Place test files next to source files (`*.spec.ts`)
- Test file naming: `component.spec.ts`
- Use descriptive test names
- Follow AAA pattern (Arrange, Act, Assert)

### Integration Tests
- Place in `test/` folder
- Test realistic user scenarios
- Mock external dependencies

### E2E Tests
- Place in `e2e/` folder
- Test critical user paths
- Use Page Object Model pattern

## Documentation

### When to Update Docs

- Adding new features → Update README and relevant docs
- Changing architecture → Update `docs/ARCHITECTURE.md`
- New configuration → Document in appropriate file
- Breaking changes → Update migration guide

### Documentation Standards

- Use clear, concise language
- Provide code examples
- Keep docs up to date
- Add links to external resources

## Pull Request Process

1. **Ensure all checks pass**
   - Linting
   - Type checking
   - Tests (when implemented)
   - Build succeeds

2. **Update documentation**
   - README if needed
   - Architecture docs if applicable
   - Code comments for complex logic

3. **Write clear PR description**
   - What changed
   - Why the change was made
   - How to test

4. **Request review**
   - Tag relevant reviewers
   - Respond to feedback
   - Make requested changes

5. **Merge**
   - Squash and merge (for clean history)
   - Delete branch after merge

## Getting Help

- **Documentation:** Start with README and docs/
- **Issues:** Check existing issues before creating new ones
- **Questions:** Open a discussion or issue
- **Real-time:** Join our Discord (if available)

## Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Focus on the code, not the person
- Help others learn and grow

## License

By contributing, you agree that your contributions will be licensed under the project's license.

## Thank You!

Your contributions make this project better. Thank you for being part of the community! 🎉
