# 🚀 Modern Full-Stack Monorepo Boilerplate

A production-ready monorepo boilerplate for building scalable full-stack applications with Next.js and NestJS.

[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-16-black.svg)](https://nextjs.org/)
[![NestJS](https://img.shields.io/badge/NestJS-11-red.svg)](https://nestjs.com/)
[![Biome](https://img.shields.io/badge/Biome-2.3-60a5fa.svg)](https://biomejs.dev/)
[![Turborepo](https://img.shields.io/badge/Turborepo-2.6-EF4444.svg)](https://turbo.build/repo)
[![pnpm](https://img.shields.io/badge/pnpm-10-orange.svg)](https://pnpm.io/)
[![CI](https://img.shields.io/badge/CI-GitHub_Actions-2088FF.svg)](https://github.com/features/actions)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## ✨ Features

### 🏗️ **Architecture**
- **Monorepo Setup** with Turborepo for efficient build orchestration
- **Shared TypeScript Configurations** - DRY principle across all packages
- **Workspace Protocol** for seamless code sharing
- **Git Hooks** with Husky for automated quality checks

### 🎯 **Frontend** (Next.js 16)
- ⚡ **App Router** - Modern file-based routing
- 🎨 **Tailwind CSS 4** - Utility-first CSS framework
- ⚛️ **React 19** - Latest React features
- 📱 **Responsive** - Mobile-first design ready
- 🔥 **Hot Module Replacement** - Lightning-fast dev experience

### 🔧 **Backend** (NestJS 11)
- 🛡️ **TypeScript-first** - End-to-end type safety
- 📦 **Modular Architecture** - Scalable and maintainable
- 🔌 **Dependency Injection** - Built-in DI container
- 🧪 **Testing Ready** - Jest configured out of the box
- 🏥 **Health Check Endpoint** - Monitor service health
- 🌐 **CORS Enabled** - Configured for frontend/backend communication
- ⚙️ **Environment Variables** - Type-safe configuration

### 🛠️ **Developer Experience**
- ⚡ **Biome** - 25x faster than ESLint/Prettier combined
- 🔄 **Auto-formatting** on save (VS Code)
- 🎣 **Pre-commit hooks** - Lint and format automatically
- 📝 **Consistent code style** across the entire codebase
- 🚀 **Parallel task execution** with Turborepo

### 📦 **Package Management**
- **pnpm** - Fast, disk space efficient
- **Workspace dependencies** - Share code between packages
- **Shared configs** - TypeScript, Biome, and more

### 🔄 **CI/CD & Automation**
- ✅ **GitHub Actions** - Automated testing and quality checks
- 🔍 **Continuous Integration** - Lint, type-check, and build on every PR
- 🧪 **Automated Testing** - Unit and E2E test workflows (ready for tests)
- 🎣 **Git Hooks** - Pre-commit validation with Husky + lint-staged

---

## 📋 Table of Contents

- [Quick Start](#-quick-start)
- [What's Included](#-whats-included)
- [Project Structure](#-project-structure)
- [Tech Stack](#-tech-stack)
- [Development](#-development)
- [Scripts](#-scripts)
- [Documentation](#-documentation)
- [Why This Stack?](#-why-this-stack)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚀 Quick Start

### Prerequisites

- **Node.js** 18+ ([Download](https://nodejs.org/))
- **pnpm** 10+ ([Install](https://pnpm.io/installation))
- **Git** ([Download](https://git-scm.com/))

### Installation

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
   - Search for "Biome" in extensions
   - Install `biomejs.biome`
   - Reload VS Code

4. **Set up environment variables**
   ```bash
   # Frontend
   cp services/acttory-fe/.env.example services/acttory-fe/.env

   # Backend
   cp services/acttory-be/.env.example services/acttory-be/.env
   ```

   Edit the `.env` files if you need to change any values.

5. **Start development servers**

   **Terminal 1 - Frontend:**
   ```bash
   cd services/acttory-fe
   pnpm dev
   ```
   Opens at [http://localhost:3000](http://localhost:3000)

   **Terminal 2 - Backend:**
   ```bash
   cd services/acttory-be
   pnpm start:dev
   ```
   Runs at [http://localhost:3001](http://localhost:3001)

6. **Verify setup**
   ```bash
   pnpm lint        # Check code quality
   pnpm build       # Build all packages
   ```

That's it! You're ready to start building. 🎉

---

## 📦 What's Included

### Services
- **acttory-fe** - Next.js 16 frontend application
- **acttory-be** - NestJS 11 backend API

### Shared Packages
- **@acttory/tsconfig** - Shared TypeScript configurations
  - `base.json` - Common settings for all projects
  - `nextjs.json` - Optimized for Next.js
  - `node.json` - Optimized for NestJS/Node.js
  - `library.json` - For shared libraries

### Development Tools
- **Biome** - Ultra-fast linting and formatting
- **Husky** - Git hooks for automation
- **lint-staged** - Run linters on staged files
- **Turborepo** - Monorepo build system

### Configuration Files
- `.vscode/settings.json` - VS Code integration
- `biome.json` - Biome configuration
- `turbo.json` - Turborepo tasks
- `pnpm-workspace.yaml` - Workspace definition
- `.editorconfig` - Editor consistency
- `.env.example` - Environment variable templates (in each service)
- `.github/workflows/` - GitHub Actions CI/CD pipelines

---

## 🗂️ Project Structure

```
acttory/
├── packages/                    # Shared packages
│   └── tsconfig/               # Shared TypeScript configs
│       ├── base.json           # Common settings
│       ├── nextjs.json         # For Next.js apps
│       ├── node.json           # For Node.js/NestJS apps
│       └── library.json        # For shared libraries
│
├── services/                    # Applications
│   ├── acttory-be/             # NestJS Backend
│   │   ├── src/
│   │   │   ├── main.ts         # Entry point + CORS setup
│   │   │   ├── app.module.ts   # Root module
│   │   │   ├── app.controller.ts # Routes + health check
│   │   │   └── app.service.ts
│   │   ├── test/               # E2E tests
│   │   └── .env.example        # Environment template
│   │
│   └── acttory-fe/             # Next.js Frontend
│       ├── src/
│       │   └── app/            # App router
│       │       ├── layout.tsx  # Root layout
│       │       ├── page.tsx    # Homepage
│       │       └── globals.css # Global styles
│       ├── public/             # Static assets
│       └── .env.example        # Environment template
│
├── docs/                        # Documentation
│   ├── ARCHITECTURE.md         # Architecture overview
│   ├── CONTRIBUTING.md         # Contribution guide
│   └── BIOME_VS_ESLINT.md     # Linting decision
│
├── .github/                     # GitHub configuration
│   └── workflows/              # CI/CD pipelines
│       ├── ci.yml              # Lint, type-check, build
│       └── test.yml            # Automated testing
│
├── .vscode/                     # VS Code settings
├── .editorconfig                # Editor consistency
├── biome.json                   # Biome config
├── turbo.json                   # Turborepo config
├── pnpm-workspace.yaml          # pnpm workspace
├── LICENSE                      # MIT license
└── package.json                 # Root package
```

---

## 🛠️ Tech Stack

### Frontend
| Technology | Version | Purpose |
|------------|---------|---------|
| [Next.js](https://nextjs.org/) | 16.0.3 | React framework with SSR |
| [React](https://react.dev/) | 19.2.0 | UI library |
| [Tailwind CSS](https://tailwindcss.com/) | 4.1.17 | Utility-first CSS |
| [TypeScript](https://www.typescriptlang.org/) | 5.9.2 | Type safety |

### Backend
| Technology | Version | Purpose |
|------------|---------|---------|
| [NestJS](https://nestjs.com/) | 11.0.1 | Node.js framework |
| [Express](https://expressjs.com/) | 5.0.0 | HTTP server |
| [TypeScript](https://www.typescriptlang.org/) | 5.7.3 | Type safety |
| [Jest](https://jestjs.io/) | 30.0.0 | Testing framework |

### Development Tools
| Tool | Version | Purpose |
|------|---------|---------|
| [Turborepo](https://turbo.build/repo) | 2.6.1 | Monorepo build system |
| [pnpm](https://pnpm.io/) | 10.0.0 | Package manager |
| [Biome](https://biomejs.dev/) | 2.3.5 | Linting & formatting |
| [Husky](https://typicode.github.io/husky/) | 9.1.7 | Git hooks |

---

## 💻 Development

### Running Services

**Frontend Development:**
```bash
cd services/acttory-fe
pnpm dev
```

**Backend Development:**
```bash
cd services/acttory-be
pnpm start:dev
```

**Watch Mode** (auto-restart on changes):
```bash
pnpm start:dev  # Backend
pnpm dev        # Frontend
```

### Building

**Build All Packages:**
```bash
pnpm build
```

**Build Specific Service:**
```bash
pnpm --filter acttory-fe build
pnpm --filter acttory-be build
```

### Linting & Formatting

**Check for issues:**
```bash
pnpm lint
```

**Auto-fix issues:**
```bash
pnpm lint:fix
```

**Type checking:**
```bash
pnpm check-types
```

### Testing

**Backend (Ready):**
```bash
cd services/acttory-be
pnpm test              # Run unit tests
pnpm test:e2e          # Run E2E tests
pnpm test:cov          # Coverage report
```

**Frontend (Add Playwright):**
```bash
cd services/acttory-fe
# Install Playwright first: pnpm add -D @playwright/test
pnpm test:e2e          # Run E2E tests (after setup)
```

**CI/CD:**
- Tests run automatically on every push and PR via GitHub Actions
- Workflows gracefully skip if tests aren't configured yet

### API Endpoints

The backend includes the following endpoints:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Welcome message |
| `/health` | GET | Health check endpoint (status, uptime, environment) |

**Example:**
```bash
# Health check
curl http://localhost:3001/health

# Response:
{
  "status": "ok",
  "timestamp": "2025-01-16T12:00:00.000Z",
  "uptime": 123.45,
  "environment": "development"
}
```

---

## 📜 Scripts

### Root Level

| Command | Description |
|---------|-------------|
| `pnpm install` | Install all dependencies |
| `pnpm dev` | Start all services (future) |
| `pnpm build` | Build all packages |
| `pnpm lint` | Check code quality |
| `pnpm lint:fix` | Fix linting issues |
| `pnpm check-types` | TypeScript type checking |
| `pnpm format` | Format all files |

### Service Level

**Frontend (`services/acttory-fe`):**
| Command | Description |
|---------|-------------|
| `pnpm dev` | Start dev server |
| `pnpm build` | Build for production |
| `pnpm start` | Start production server |
| `pnpm lint` | Lint this package |
| `pnpm check-types` | Type check |

**Backend (`services/acttory-be`):**
| Command | Description |
|---------|-------------|
| `pnpm start:dev` | Start dev server |
| `pnpm build` | Build for production |
| `pnpm start:prod` | Start production server |
| `pnpm test` | Run tests |
| `pnpm test:e2e` | Run E2E tests |

---

## 📚 Documentation

- **[Architecture Overview](./docs/ARCHITECTURE.md)** - System design and structure
- **[Contributing Guide](./docs/CONTRIBUTING.md)** - How to contribute
- **[Biome vs ESLint](./docs/BIOME_VS_ESLINT.md)** - Why we chose Biome

---

## 🤔 Why This Stack?

### Why Monorepo?
✅ **Code Sharing** - Share types, utils, configs across services
✅ **Atomic Commits** - Change frontend and backend together
✅ **Consistent Tooling** - Same linting, formatting everywhere
✅ **Simplified Deps** - Single `node_modules` at root

[Read more in docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md#why-monorepo)

### Why Turborepo?
✅ **Speed** - Parallel execution + intelligent caching
✅ **DX** - Simple configuration, powerful features
✅ **Scalability** - Grows with your project
✅ **Remote Caching** - Share cache across team (optional)

### Why Biome?
✅ **Performance** - 25x faster than Prettier, 15x faster than ESLint
✅ **Simplicity** - One tool instead of multiple
✅ **Zero Config** - Works out of the box
✅ **Active Development** - Modern, well-maintained

[Read detailed comparison](./docs/BIOME_VS_ESLINT.md)

### Why Next.js + NestJS?
✅ **Type Safety** - End-to-end TypeScript
✅ **Best Practices** - Battle-tested frameworks
✅ **Developer Experience** - Amazing DX
✅ **Production Ready** - Used by thousands of companies

### Why Shared TypeScript Configs?
✅ **DRY Principle** - Configure once, use everywhere
✅ **Consistency** - Same strict rules across codebase
✅ **Maintainability** - Update in one place
✅ **Best Practices** - Enforced automatically

---

## 🗺️ Roadmap

### ✅ Phase 1: Foundation (Complete)
- [x] Monorepo setup with Turborepo
- [x] Next.js frontend
- [x] NestJS backend
- [x] Shared TypeScript configs
- [x] Biome linting & formatting
- [x] Git hooks automation
- [x] Environment variable management
- [x] Health check endpoint
- [x] CORS configuration
- [x] CI/CD pipeline (GitHub Actions)
- [x] EditorConfig for consistency
- [x] MIT License

### 🚧 Phase 2: Core Features (Next Up)
- [ ] Database integration (Prisma)
- [ ] Authentication (JWT/Sessions)
- [ ] API client setup
- [ ] Shared types package
- [ ] Docker configuration
- [ ] Testing infrastructure (Jest/Playwright)

### 📋 Phase 3: Enhanced DX (Planned)
- [ ] shadcn/ui component library
- [ ] Shared UI components package
- [ ] Shared utilities package
- [ ] Storybook for components
- [ ] API documentation (Swagger)
- [ ] Deployment configurations

### 🚀 Phase 4: Production Ready (Future)
- [ ] Monitoring & logging
- [ ] Performance optimization
- [ ] Security hardening
- [ ] Documentation site
- [ ] Multi-environment setup
- [ ] Rate limiting

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](./docs/CONTRIBUTING.md) for details.

### Quick Contribution Steps

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

Built with amazing open-source projects:
- [Next.js](https://nextjs.org/) by Vercel
- [NestJS](https://nestjs.com/) by Kamil Myśliwiec
- [Biome](https://biomejs.dev/) by Biome team
- [Turborepo](https://turbo.build/) by Vercel
- [pnpm](https://pnpm.io/) by pnpm contributors

---

## 📞 Support

- **Documentation:** Check [docs/](./docs) folder
- **Issues:** [GitHub Issues](https://github.com/your-username/acttory/issues)
- **Discussions:** [GitHub Discussions](https://github.com/your-username/acttory/discussions)

---

## ⭐ Show Your Support

If this boilerplate helped you, please give it a ⭐ on GitHub!

---

<div align="center">

**[Documentation](./docs)** • **[Contributing](./docs/CONTRIBUTING.md)** • **[License](LICENSE)**

Made with ❤️ by developers, for developers

</div>
