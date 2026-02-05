# Antigravity PRD Generator - Step 1: Analyze Codebase

You are working on an existing ERP system. Before generating a PRD for new features, you must first understand the existing codebase structure, patterns, and conventions.

## Your Task

Analyze the codebase and document everything in `CODEBASE_ANALYSIS.md`. This will be used to generate accurate PRDs later.

## What to Document

### 1. Project Structure

```
- Where are components located?
- Where are API routes/controllers?
- Where are database models/schemas?
- Where are utilities/helpers?
- Where are types/interfaces?
```

### 2. Tech Stack (Already Known)

**Frontend:**

- React 19.2 with TypeScript
- Vite build tool
- React Router 7.12
- TanStack Query (React Query) for data fetching
- TanStack Table for tables
- React Hook Form + Zod for forms/validation
- Radix UI components
- Tailwind CSS 4.x
- Lucide React icons
- date-fns for dates
- Recharts for charts
- Sonner/React Hot Toast for notifications

**Backend:**

- Node.js with TypeScript
- Express 5.x
- Prisma ORM 7.3 with PostgreSQL
- JWT authentication (jsonwebtoken)
- Argon2 for password hashing
- Express rate limiting
- Helmet for security
- CORS enabled
- Node-cron for scheduled tasks

**Build Tools:**

- pnpm package manager
- tsx for development (watch mode)
- TypeScript 5.9

### 3. Code Patterns to Document

**Frontend Patterns:**

- How are components organized? (pages/, components/, features/)
- Component naming conventions?
- How is state managed? (Context, React Query, local state?)
- How are API calls made? (axios with React Query?)
- Form pattern (React Hook Form + Zod schema?)
- How are routes structured?
- UI component library usage (Radix UI + Tailwind?)

**Backend Patterns:**

- How are routes organized? (routes/, controllers/, services?)
- Authentication middleware pattern?
- How is validation done? (Zod schemas?)
- Error handling pattern?
- Prisma model naming conventions?
- How are migrations managed? (prisma migrate dev)
- API response format?

**Database Patterns:**

- Prisma schema location? (prisma/schema.prisma)
- Naming conventions for tables/models?
- How are relationships defined?
- How are enums handled?
- Seeding pattern? (prisma db seed)

### 4. Existing Features to Document

Look at the codebase and list what's already implemented:

- User authentication system?
- Employee management?
- Department/organization structure?
- Time tracking/clock in-out?
- Leave/attendance system?
- Payroll system?
- Reports/analytics?
- Role-based access control?

### 5. Important Files to Note

- Environment variables (.env pattern)
- Configuration files
- Middleware structure
- Utility functions location
- Type definitions location
- Constants/enums location

### 6. Quality Standards

- Linting rules (ESLint config)
- TypeScript strictness
- Testing setup (if any)
- Code formatting (Prettier?)

### 7. Common Gotchas

- Any special conventions?
- Things to avoid?
- Required patterns?
- Performance considerations?

## Output Format

Create `CODEBASE_ANALYSIS.md` with this structure:

```markdown
# ERP System - Codebase Analysis

Last Updated: [DATE]

## Project Overview

[Brief description of what the ERP system does]

## Tech Stack

[List from package.json - already documented above]

## Frontend Structure

### Directory Layout
```

src/
├── components/ [Purpose]
├── pages/ [Purpose]
├── hooks/ [Purpose]
├── utils/ [Purpose]
└── ...

```

### Component Patterns
- Component files: `ComponentName.tsx`
- Styling: Tailwind classes with CVA for variants
- State: React Query for server state, useState for local
- Forms: React Hook Form + Zod schema validation
- [Add more patterns you discover]

### API Integration
- Base URL: [from config]
- API client: axios with React Query hooks
- Auth: JWT in cookies/headers
- [Pattern examples]

## Backend Structure

### Directory Layout
```

src/
├── routes/ [Purpose]
├── controllers/ [Purpose]
├── services/ [Purpose]
├── middleware/ [Purpose]
└── ...

```

### API Patterns
- Routes: `/api/resource` or `/api/v1/resource`
- Controllers: Handle request/response
- Services: Business logic
- Validation: Zod schemas in routes/controllers
- Auth: JWT middleware
- [Add patterns you discover]

### Database (Prisma)
- Schema: `prisma/schema.prisma`
- Models: PascalCase (User, Employee, Department)
- Migrations: `pnpm prisma:migrate`
- Seeding: `pnpm db:seed`
- [Add conventions you discover]

## Existing Features

### Authentication
- [How it works, what's implemented]

### Employee Management
- [What exists]

### [Other Features]
- [Document each major feature area]

## Conventions & Standards

### Naming
- Files: [Convention]
- Components: [Convention]
- Functions: [Convention]
- Database: [Convention]

### Code Style
- ESLint rules
- TypeScript strict mode
- [Other standards]

## Important Patterns

### Authentication Flow
[Describe how auth works from login to protected routes]

### Data Fetching Pattern
[Example of typical CRUD operation]

### Form Handling Pattern
[Example form with validation]

### Error Handling
[Frontend and backend error patterns]

## Common Utilities

### Frontend
- [List common hooks, utils]

### Backend
- [List common middleware, helpers]

## Database Schema Highlights

### Key Models
- User
- Employee
- Department
- [List important models and relationships]

## API Endpoints (Existing)

### Auth
- POST /api/auth/login
- POST /api/auth/logout
- [List others]

### Employees
- [List endpoints]

### [Other Resources]
- [List endpoints]

## Environment Setup

### Required Environment Variables
```

DATABASE_URL=
JWT_SECRET=
[List others]

````

### Development Commands
```bash
# Frontend
pnpm dev

# Backend
pnpm dev

# Database
pnpm prisma:migrate
pnpm prisma:studio
````

## Gotchas & Notes

- [Any special things to remember]
- [Common mistakes to avoid]
- [Performance considerations]
- [Security patterns]

```

## How to Run This Analysis

1. Explore the entire codebase systematically
2. Look at actual code files for patterns
3. Check existing features
4. Document everything in CODEBASE_ANALYSIS.md
5. Be thorough - this is the foundation for all future PRD generation

Once this analysis is complete, we can generate accurate PRDs for new features!
```
