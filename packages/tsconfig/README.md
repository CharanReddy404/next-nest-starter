# @acttory/tsconfig

Shared TypeScript configuration for the Acttory monorepo.

## Available Configurations

### 1. `base.json` - Common Settings
Base configuration inherited by all other configs.

**Contains:**
- Strict type checking
- Module resolution settings
- Common compiler options

**Don't extend this directly** - use the specific configs below instead.

---

### 2. `nextjs.json` - For Next.js Applications

**Use for:** Frontend applications using Next.js

**Example:**
```json
{
  "extends": "@acttory/tsconfig/nextjs.json",
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

**Projects using this:**
- `services/acttory-fe`

---

### 3. `node.json` - For Node.js/NestJS Applications

**Use for:** Backend services using Node.js or NestJS

**Example:**
```json
{
  "extends": "@acttory/tsconfig/node.json",
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  },
  "include": ["src/**/*"]
}
```

**Projects using this:**
- `services/acttory-be`

---

### 4. `library.json` - For Shared Packages

**Use for:** Shared TypeScript libraries (types, utils, constants)

**Perfect for:**
- `packages/types` - Shared types between FE and BE
- `packages/utils` - Shared utility functions
- `packages/constants` - Shared constants
- `packages/api-client` - API client wrapper

**Example:**
```json
{
  "extends": "@acttory/tsconfig/library.json",
  "compilerOptions": {
    "outDir": "./dist",
    "rootDir": "./src"
  }
}
```

**Why use this:**
- Works in both browser and Node.js environments
- Generates `.d.ts` type definition files
- Strict type checking for library quality
- No DOM or React dependencies (pure TypeScript)

---

## Creating a New Shared Package

### Example: Shared Types Package

1. **Create the package:**
```bash
mkdir -p packages/types/src
cd packages/types
```

2. **Create `package.json`:**
```json
{
  "name": "@acttory/types",
  "version": "0.0.0",
  "private": true,
  "main": "./dist/index.js",
  "types": "./dist/index.d.ts",
  "exports": {
    ".": {
      "types": "./dist/index.d.ts",
      "default": "./dist/index.js"
    }
  },
  "scripts": {
    "build": "tsc",
    "dev": "tsc --watch"
  },
  "devDependencies": {
    "@acttory/tsconfig": "workspace:*",
    "typescript": "^5.9.2"
  }
}
```

3. **Create `tsconfig.json`:**
```json
{
  "extends": "@acttory/tsconfig/library.json"
}
```

4. **Create types:**
```typescript
// src/user.ts
export interface User {
  id: string;
  email: string;
  name: string;
}

// src/index.ts
export * from './user';
```

5. **Build it:**
```bash
pnpm build
```

6. **Use it in other packages:**
```bash
cd ../../services/acttory-fe
pnpm add @acttory/types@workspace:*
```

```typescript
// services/acttory-fe/src/app/page.tsx
import { User } from '@acttory/types';

const user: User = { id: '1', email: 'test@test.com', name: 'John' };
```

---

## Key Differences

| Config | Use For | Has DOM? | Has React? | Emits Files? | Decorators? |
|--------|---------|----------|------------|--------------|-------------|
| `nextjs.json` | Next.js apps | ✅ Yes | ✅ Yes | ❌ No (Next.js handles it) | ❌ No |
| `node.json` | NestJS/Node apps | ❌ No | ❌ No | ✅ Yes | ✅ Yes |
| `library.json` | Shared packages | ❌ No | ❌ No | ✅ Yes | ❌ No |

---

## Benefits

✅ **Consistency** - All projects use the same TypeScript rules
✅ **Maintainability** - Change settings once, applies everywhere
✅ **Type Safety** - Strict settings catch bugs early
✅ **Scalability** - Add new packages easily
