# Architecture Overview

## Project Structure

```
acttory/
├── packages/                    # Shared packages
│   └── tsconfig/               # Shared TypeScript configurations
│       ├── base.json           # Common settings
│       ├── nextjs.json         # For Next.js apps
│       ├── node.json           # For Node.js/NestJS apps
│       └── library.json        # For shared libraries
│
├── services/                    # Applications & Services
│   ├── acttory-be/             # Backend API (NestJS)
│   └── acttory-fe/             # Frontend App (Next.js)
│
├── docs/                        # Documentation
├── .vscode/                     # VS Code settings
├── .husky/                      # Git hooks
├── biome.json                   # Biome configuration
├── turbo.json                   # Turborepo configuration
└── pnpm-workspace.yaml          # pnpm workspace configuration
```

## Technology Stack

### Frontend (`services/acttory-fe`)
- **Framework:** Next.js 16 (App Router)
- **UI Library:** React 19
- **Styling:** Tailwind CSS 4
- **Language:** TypeScript 5
- **Linting:** Biome

### Backend (`services/acttory-be`)
- **Framework:** NestJS 11
- **Runtime:** Node.js 18+
- **Language:** TypeScript 5
- **Testing:** Jest
- **Linting:** Biome

### Shared Infrastructure
- **Monorepo:** Turborepo 2.6
- **Package Manager:** pnpm 10
- **Linting & Formatting:** Biome 2.3
- **Git Hooks:** Husky + lint-staged
- **TypeScript Configs:** Shared across all packages

## Design Decisions

### Why Monorepo?
- **Code Sharing:** Share types, utilities, and configurations
- **Atomic Commits:** Make changes across frontend and backend in one commit
- **Consistent Tooling:** Same linting, formatting, and build tools everywhere
- **Simplified Dependency Management:** Single `node_modules` at root

### Why Turborepo?
- **Intelligent Caching:** Cache build outputs, never rebuild what hasn't changed
- **Parallel Execution:** Run tasks across packages in parallel
- **Task Pipelines:** Define dependencies between tasks
- **Remote Caching:** Share cache across team (optional)

### Why Biome?
- **Performance:** 25x faster than Prettier, 15x faster than ESLint
- **Simplicity:** Single tool for linting and formatting
- **Zero Config:** Works out of the box with sensible defaults
- **Active Development:** Modern tooling with fast iteration

### Why Shared TypeScript Configs?
- **DRY Principle:** Configure once, use everywhere
- **Consistency:** Same strict rules across all packages
- **Maintainability:** Update settings in one place
- **Best Practices:** Enforced across the entire codebase

## Data Flow

### Frontend → Backend Communication

```
┌─────────────────────┐
│   Next.js (Client)  │
│   services/acttory-fe│
└──────────┬──────────┘
           │
           │ HTTP Request
           │ (fetch/axios)
           ↓
┌─────────────────────┐
│   NestJS (Server)   │
│   services/acttory-be│
└─────────────────────┘
```

### Shared Types Flow

```
┌─────────────────────┐
│  packages/types     │ (Future)
│  Shared TypeScript  │
│  Interfaces          │
└──────────┬──────────┘
           │
           ├────────────────┐
           │                │
           ↓                ↓
┌──────────────────┐  ┌──────────────────┐
│  Frontend        │  │  Backend         │
│  Uses Types      │  │  Uses Types      │
│  (compile-time)  │  │  (compile-time)  │
└──────────────────┘  └──────────────────┘
```

## Build & Development Workflow

### Development
```bash
# Terminal 1: Frontend dev server
cd services/acttory-fe
pnpm dev

# Terminal 2: Backend dev server
cd services/acttory-be
pnpm start:dev
```

### Production Build
```bash
# Build all packages
pnpm build

# Or build specific service
pnpm --filter acttory-fe build
pnpm --filter acttory-be build
```

### Linting & Formatting
```bash
# Lint everything
pnpm lint

# Fix all issues
pnpm lint:fix

# Git hook runs automatically on commit
git commit -m "feat: add feature"
```

## Future Architecture

### Planned Shared Packages

```
packages/
├── tsconfig/          # ✅ Done
├── types/             # 📋 Planned - Shared TypeScript types
├── ui/                # 📋 Planned - Shared React components
├── utils/             # 📋 Planned - Shared utilities
├── constants/         # 📋 Planned - Shared constants
└── api-client/        # 📋 Planned - API client wrapper
```

### Microservices Architecture (Future)

```
services/
├── api/               # Main REST API
├── auth/              # Authentication service
├── notifications/     # Notification service
├── workers/           # Background jobs
└── websocket/         # Real-time communication
```

## Scalability Considerations

### Horizontal Scaling
- Frontend: Deploy on Vercel/CDN (stateless)
- Backend: Multiple instances behind load balancer
- Database: Read replicas, connection pooling

### Caching Strategy
- Build outputs: Turborepo cache
- API responses: Redis (future)
- Static assets: CDN

### Deployment
- Frontend: Vercel, Netlify, or CloudFlare Pages
- Backend: Docker containers on AWS/GCP/Azure
- Database: Managed PostgreSQL/MySQL

## Security

### Current Implementation
- TypeScript strict mode (type safety)
- Biome linting (catch common issues)
- Git hooks (prevent bad code)

### Future Additions
- Authentication (JWT/Sessions)
- CORS configuration
- Rate limiting
- Input validation (Zod)
- SQL injection prevention (ORM)
- XSS protection

## Performance Optimization

### Current
- Turborepo caching (build time)
- Biome (fast linting)
- pnpm (fast installs)

### Future
- Code splitting (Next.js)
- Image optimization (Next.js)
- API response caching
- Database query optimization
- Lazy loading

## Monitoring & Observability (Future)

### Logging
- Structured logging (Winston/Pino)
- Centralized log aggregation

### Metrics
- Application metrics (Prometheus)
- Business metrics (custom)

### Tracing
- Distributed tracing (OpenTelemetry)
- Performance monitoring

## Testing Strategy (Future)

### Unit Tests
- Jest for both frontend and backend
- React Testing Library for components
- Coverage targets: 80%+

### Integration Tests
- API endpoint testing (Supertest)
- Database integration tests

### E2E Tests
- Playwright/Cypress for critical user flows
- Automated browser testing

## Continuous Integration (Future)

```yaml
# Example GitHub Actions workflow
Build → Lint → Test → Deploy
  ↓       ↓      ↓       ↓
Turbo  Biome  Jest  Vercel/Docker
```

## Documentation

- **README.md** - Getting started
- **docs/ARCHITECTURE.md** - This file
- **docs/BIOME_VS_ESLINT.md** - Linting decision
- **docs/LEARNING_TODO.md** - Learning resources
- **packages/*/README.md** - Package-specific docs

## Contributing

See main README for contribution guidelines.

## Resources

- [Turborepo Handbook](https://turbo.build/repo/docs/handbook)
- [Next.js Documentation](https://nextjs.org/docs)
- [NestJS Documentation](https://docs.nestjs.com)
- [Biome Documentation](https://biomejs.dev)
- [pnpm Workspaces](https://pnpm.io/workspaces)
