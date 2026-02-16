# ANALYZE_CODEBASE.md

You are analyzing an existing codebase to understand its structure, patterns, and conventions. This analysis will be used to implement new features that seamlessly integrate with the existing code.

## Your Mission

**Explore the entire project and document everything in `CODEBASE_ANALYSIS.md`**

This is a **discovery process** - don't assume anything. Find and document what actually exists.

---

## Step 1: Detect Technology Stack

### Auto-Detect from Files

Look for these indicator files and extract tech info:

**JavaScript/TypeScript Projects:**

- `package.json` → Read dependencies to identify:
  - Frontend: React, Vue, Angular, Svelte, Next.js, etc.
  - Backend: Express, Fastify, NestJS, Koa, etc.
  - Database ORM: Prisma, TypeORM, Sequelize, Mongoose, etc.
  - Build tools: Vite, Webpack, Rollup, etc.
  - Testing: Jest, Vitest, Mocha, etc.
  - Package manager: Check `packageManager` field or lock file (pnpm-lock.yaml, yarn.lock, package-lock.json)

**Python Projects:**

- `requirements.txt` or `pyproject.toml` → Identify:
  - Framework: Django, Flask, FastAPI, etc.
  - ORM: SQLAlchemy, Django ORM, etc.
  - Testing: pytest, unittest, etc.

**Java Projects:**

- `pom.xml` (Maven) or `build.gradle` (Gradle) → Identify:
  - Framework: Spring Boot, Jakarta EE, etc.
  - Database: JPA, Hibernate, etc.

**PHP Projects:**

- `composer.json` → Identify:
  - Framework: Laravel, Symfony, etc.

**Go Projects:**

- `go.mod` → Identify frameworks and libraries

**Ruby Projects:**

- `Gemfile` → Identify Rails, Sinatra, etc.

**Database Detection:**

- Check for: `prisma/schema.prisma`, `migrations/`, `database.sql`, etc.
- Read connection strings from config files
- Identify: PostgreSQL, MySQL, MongoDB, SQLite, etc.

**Infrastructure:**

- `Dockerfile` → Docker usage
- `docker-compose.yml` → Multi-container setup
- `.github/workflows/` → GitHub Actions
- `vercel.json`, `netlify.toml` → Deployment platform

---

## Step 2: Map Project Structure

### Directory Analysis

Explore the entire project tree and identify:

**Frontend Structure:**

```
Where are components? (src/components, app/components, components/, etc.)
Where are pages/routes? (src/pages, app/, pages/, routes/, etc.)
Where are styles? (src/styles, styles/, CSS-in-JS, Tailwind, etc.)
Where are hooks/composables? (src/hooks, hooks/, composables/, etc.)
Where are utilities? (src/utils, lib/, helpers/, etc.)
Where are types/interfaces? (src/types, types/, @types/, etc.)
Where are assets? (public/, assets/, static/, etc.)
```

**Backend Structure:**

```
Where are routes? (src/routes, routes/, api/, controllers/, etc.)
Where are controllers? (src/controllers, controllers/, handlers/, etc.)
Where are services? (src/services, services/, domain/, etc.)
Where are models? (src/models, models/, entities/, etc.)
Where are middleware? (src/middleware, middleware/, guards/, etc.)
Where are database files? (prisma/, migrations/, database/, etc.)
Where are tests? (tests/, __tests__, src/__tests__, spec/, etc.)
```

**Monorepo Detection:**

```
Is this a monorepo? (packages/, apps/, check for lerna.json, nx.json, turbo.json)
What workspaces exist?
How are they organized?
```

---

## Step 3: Identify Code Patterns

### Analyze Existing Code

**Look at actual files** to discover patterns:

**Component Patterns (Frontend):**

```
- File naming: PascalCase.tsx, kebab-case.vue, etc.
- Component structure: Functional components? Class components?
- Props: TypeScript interfaces? PropTypes?
- State management: useState, Redux, Zustand, Pinia, MobX, etc.
- Styling: CSS Modules, Styled Components, Tailwind, Emotion, etc.
- Folder structure: Flat? Grouped by feature? Atomic design?
```

**API Patterns (Backend):**

```
- Route definition: Express router, decorators, file-based routing?
- Request validation: Zod, Joi, class-validator, etc.
- Response format: { data: ... }, { success, data }, etc.
- Error handling: Try/catch? Error middleware? Custom error classes?
- Authentication: JWT? Sessions? Passport? Custom?
- Authorization: RBAC? Permissions? Guards?
```

**Database Patterns:**

```
- ORM/Query builder: Prisma, TypeORM, Sequelize, Knex, raw SQL?
- Model naming: PascalCase, snake_case, etc.
- Relationships: How are they defined?
- Migrations: How are they managed?
- Seeding: How is initial data loaded?
```

**Testing Patterns:**

```
- Test files location: __tests__, *.test.ts, *.spec.ts?
- Testing library: Jest, Vitest, Mocha, pytest, JUnit?
- Mocking: How are dependencies mocked?
- Coverage: Is there a coverage threshold?
```

---

## Step 4: Document Conventions

### Code Style & Standards

**Naming Conventions:**

```
- Variables: camelCase, snake_case?
- Functions: camelCase, snake_case?
- Classes: PascalCase?
- Constants: UPPER_CASE, camelCase?
- Files: PascalCase, kebab-case, snake_case?
- Folders: kebab-case, camelCase?
```

**Code Organization:**

```
- Imports order: Built-in, external, internal?
- Export style: Named exports, default exports?
- File length limits?
- Function length limits?
```

**Configuration:**

```
- ESLint/Prettier: Check .eslintrc, .prettierrc
- TypeScript: Check tsconfig.json (strict mode? paths?)
- Linting rules: What's enforced?
```

---

## Step 5: Find Existing Features

### Feature Inventory

**Explore the codebase to find what's already built:**

**Authentication & Authorization:**

```
- Login/logout system?
- Registration?
- Password reset?
- Role-based access control?
- Permissions system?
```

**Core Modules:**

```
- User management?
- Dashboard?
- Settings/configuration?
- Reports/analytics?
- Notifications?
```

**Domain-Specific Features:**

```
What is this app about? E-commerce? CRM? ERP? SaaS?
What features already exist?
What models/entities are in the database?
```

---

## Step 6: Identify Integration Points

### External Services & APIs

**Check for integrations:**

```
- Payment gateways? (Stripe, PayPal, etc.)
- Email services? (SendGrid, AWS SES, etc.)
- File storage? (AWS S3, Cloudinary, etc.)
- Analytics? (Google Analytics, Mixpanel, etc.)
- Authentication providers? (OAuth, Auth0, etc.)
- APIs consumed? (Third-party services)
```

---

## Step 7: Development Workflow

### Build & Deploy Process

**Document how things work:**

**Commands:**

```bash
# Find from package.json scripts or Makefile
How to start dev server?
How to build for production?
How to run tests?
How to run linting?
How to run type checking?
How to run migrations?
```

**Environment Setup:**

```
What .env variables are needed?
Where is example .env file?
How is configuration managed?
```

**Deployment:**

```
How is the app deployed?
What platforms? (Vercel, AWS, Heroku, etc.)
CI/CD pipeline? (GitHub Actions, GitLab CI, etc.)
```

---

## Output Format: CODEBASE_ANALYSIS.md

Create a file `Ralph/CODEBASE_ANALYSIS.md` with this exact structure:

```markdown
# Codebase Analysis

**Last Updated:** [Date]
**Project Type:** [Web App / Mobile App / API / CLI / etc.]

---

## Technology Stack

### Core Technologies

- **Language:** [JavaScript/TypeScript/Python/Java/etc.]
- **Runtime/Platform:** [Node.js 20.x / Python 3.11 / JVM 17 / etc.]
- **Package Manager:** [pnpm / npm / yarn / pip / maven / etc.]

### Frontend (if applicable)

- **Framework:** [React 19 / Vue 3 / Angular / Svelte / etc.]
- **Build Tool:** [Vite / Webpack / Next.js / etc.]
- **UI Library:** [Radix UI / Material-UI / Ant Design / etc.]
- **Styling:** [Tailwind CSS / CSS Modules / Styled Components / etc.]
- **State Management:** [TanStack Query / Redux / Zustand / etc.]
- **Routing:** [React Router / Next.js / Vue Router / etc.]
- **Forms:** [React Hook Form / Formik / etc.]
- **Validation:** [Zod / Yup / etc.]

### Backend (if applicable)

- **Framework:** [Express / NestJS / FastAPI / Spring Boot / etc.]
- **Database:** [PostgreSQL / MySQL / MongoDB / etc.]
- **ORM/Query Builder:** [Prisma / TypeORM / Sequelize / etc.]
- **Authentication:** [JWT / Sessions / Passport / etc.]
- **Validation:** [Zod / class-validator / etc.]

### Testing

- **Test Framework:** [Jest / Vitest / pytest / JUnit / etc.]
- **E2E Testing:** [Playwright / Cypress / none]

### DevOps

- **Containerization:** [Docker / none]
- **CI/CD:** [GitHub Actions / GitLab CI / none]
- **Deployment:** [Vercel / AWS / Heroku / etc.]

---

## Project Structure

### Frontend Structure

\`\`\`
[Paste actual directory tree from src/ or app/]
\`\`\`

**Key Directories:**

- Components: `[path]` - [Description of organization]
- Pages/Routes: `[path]` - [How routing works]
- Hooks: `[path]` - [Reusable hooks location]
- Utils: `[path]` - [Helper functions]
- Types: `[path]` - [TypeScript definitions]
- Styles: `[path]` - [Global styles, themes]

### Backend Structure

\`\`\`
[Paste actual directory tree from src/ or app/]
\`\`\`

**Key Directories:**

- Routes: `[path]` - [API route definitions]
- Controllers: `[path]` - [Request handlers]
- Services: `[path]` - [Business logic]
- Models: `[path]` - [Data models]
- Middleware: `[path]` - [Auth, validation, etc.]
- Database: `[path]` - [Migrations, seeds, schema]

### Database

- **Schema Location:** `[path to schema file]`
- **Migrations:** `[how migrations are managed]`
- **Seeding:** `[how seed data is loaded]`

---

## Code Patterns

### Component Pattern (Frontend)

\`\`\`tsx
// Example from actual codebase
[Paste a real component showing the pattern]
\`\`\`

**Key Observations:**

- File naming: [Convention found]
- Component style: [Functional/Class, hooks used]
- Props: [How props are typed]
- State: [How state is managed]
- Styling: [How components are styled]

### API Pattern (Backend)

\`\`\`typescript
// Example from actual codebase
[Paste a real route/controller showing the pattern]
\`\`\`

**Key Observations:**

- Route structure: [How routes are organized]
- Validation: [How requests are validated]
- Response format: [Standard response shape]
- Error handling: [How errors are handled]
- Authentication: [How auth is applied]

### Database Pattern

\`\`\`prisma
// Example model from schema
[Paste a real model]
\`\`\`

**Key Observations:**

- Naming: [Convention found]
- Relationships: [How relations are defined]
- Indexes: [Index strategy]
- Enums: [How enums are used]

---

## Naming Conventions

**Files:**

- Components: `[PascalCase.tsx / kebab-case.vue / etc.]`
- Utils: `[camelCase.ts / snake_case.py / etc.]`
- Types: `[PascalCase.ts / etc.]`

**Code:**

- Variables: `[camelCase / snake_case]`
- Functions: `[camelCase / snake_case]`
- Classes: `[PascalCase]`
- Constants: `[UPPER_CASE / camelCase]`

**Database:**

- Tables: `[PascalCase / snake_case]`
- Columns: `[camelCase / snake_case]`
- Relations: `[How named]`

---

## Existing Features

### Authentication

[✓ Implemented / ✗ Not present]

- Login/Logout
- Registration
- Password reset
- Session management
- Role-based access

### Core Features

[List major features found in the codebase]

- [Feature 1]
- [Feature 2]
- [Feature 3]

### Database Models

[List key models/entities found]

- User
- [Other models]

---

## Development Commands

\`\`\`bash

# Development

[command to start dev server]

# Build

[command to build for production]

# Testing

[command to run tests]

# Linting

[command to lint code]

# Type Checking

[command for type check]

# Database

[command to run migrations]
[command to generate types/client]
[command to seed database]
\`\`\`

---

## Environment Variables

**Required variables:**
\`\`\`
[List from .env.example or actual usage]
DATABASE_URL=
JWT_SECRET=
[etc.]
\`\`\`

---

## Quality Standards

**Linting:**

- Config: `[.eslintrc.js / .eslintrc.json / etc.]`
- Rules: [Strict / Recommended / Custom]

**TypeScript:**

- Strict mode: [Yes / No]
- Target: [ES2020 / ES2022 / etc.]

**Testing:**

- Coverage threshold: [X% / none]
- Required for: [All features / none]

---

## Important Patterns & Gotchas

### DO's (Patterns to follow)

- [Pattern 1 discovered]
- [Pattern 2 discovered]
- [Pattern 3 discovered]

### DON'Ts (Things to avoid)

- [Antipattern 1 found]
- [Antipattern 2 found]

### Gotchas

- [Gotcha 1]
- [Gotcha 2]

---

## Integration Points

**External Services:**

- [Service 1]: [How it's used]
- [Service 2]: [How it's used]

**APIs Consumed:**

- [API 1]: [Purpose]

---

## Notes for Future Implementation

[Any additional observations that would help implement new features]

---

**Analysis Complete!** ✓

This document should be kept updated as the codebase evolves.
```

---

## Critical Instructions

1. **EXPLORE FIRST** - Don't assume anything. Look at actual files.

2. **BE THOROUGH** - Check every major directory and file type.

3. **USE REAL EXAMPLES** - Paste actual code snippets from the project.

4. **BE ACCURATE** - If you can't find something, say "Not found" - don't guess.

5. **UPDATE ANALYSIS** - If you discover something new later, update CODEBASE_ANALYSIS.md

---

## How to Run

```
Read this file (ANALYZE_CODEBASE.md) and perform a complete codebase analysis. Create CODEBASE_ANALYSIS.md with all findings.
```

Start with package.json, requirements.txt, or similar dependency files to identify the tech stack, then explore from there.
