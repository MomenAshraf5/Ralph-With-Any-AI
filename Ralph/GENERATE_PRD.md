# GENERATE_PRD.md

You are generating a Product Requirements Document (PRD) for a new feature. This PRD must integrate seamlessly with the existing codebase patterns documented in `CODEBASE_ANALYSIS.md`.

## Your Mission

Generate `prd.json` - a structured list of user stories that break down the feature into implementable chunks.

---

## Prerequisites

**BEFORE generating the PRD:**

1. ✅ Read `CODEBASE_ANALYSIS.md` thoroughly
2. ✅ Understand the tech stack
3. ✅ Know the existing patterns
4. ✅ Identify integration points

**If CODEBASE_ANALYSIS.md doesn't exist** → Run ANALYZE_CODEBASE.md first!

---

## Input: Feature Request

The user will provide a feature description. Examples:

```
Feature: User Profile Management
- Users can view/edit their profile
- Upload profile picture
- Change password
- View activity history
```

```
Feature: Export Reports to PDF
- Generate PDF reports
- Include charts and tables
- Email reports to users
```

---

## Output: prd.json Structure

```json
{
  "feature": {
    "name": "User Profile Management",
    "description": "Allow users to manage their profile information",
    "branch": "feature/user-profile-management"
  },
  
  "techContext": {
    "frontend": "[From CODEBASE_ANALYSIS.md]",
    "backend": "[From CODEBASE_ANALYSIS.md]",
    "database": "[From CODEBASE_ANALYSIS.md]"
  },
  
  "integrationPoints": [
    "Existing authentication system",
    "File upload service",
    "User model"
  ],
  
  "stories": [
    {
      "id": "profile-001",
      "template": "database_model",
      "title": "Extend User model for profile data",
      "description": "Add profile-related fields to existing User model",
      "priority": 1,
      "estimatedComplexity": "small",
      "passes": false,
      
      "acceptanceCriteria": [
        "Database schema updated with new fields",
        "Migration created and tested",
        "ORM types regenerated"
      ],
      
      "technicalNotes": [
        "Follow existing model patterns from CODEBASE_ANALYSIS.md",
        "Use same naming convention as other models",
        "Add indexes for frequently queried fields"
      ],
      
      "filesExpected": [
        "migrations/XXX_add_profile_fields.sql",
        "Update schema file"
      ]
    }
  ],
  
  "assumptions": [
    "User authentication already exists",
    "File storage system is configured"
  ],
  
  "outOfScope": [
    "Social media login integration",
    "Public profile pages"
  ]
}
```

---

## Story Templates

Use these templates as starting points. **Adapt to the actual tech stack** from CODEBASE_ANALYSIS.md.

### Template: `database_model`

**When to use:** Creating or modifying database tables/models

**Story structure:**
```json
{
  "id": "[feature]-001",
  "template": "database_model",
  "title": "Create/Update [ModelName] model",
  "priority": 1,
  "acceptanceCriteria": [
    "Schema file updated with model definition",
    "Migration created (if applicable)",
    "Model includes: [list required fields]",
    "Relationships defined: [list relations]",
    "Indexes added on: [list indexed fields]",
    "Migration runs successfully",
    "ORM types/client regenerated"
  ],
  "technicalNotes": [
    "Follow naming convention: [from CODEBASE_ANALYSIS]",
    "Use [ORM name] from existing setup",
    "Match relationship pattern from existing models"
  ]
}
```

**Adapt for:**
- Prisma: "Update prisma/schema.prisma, run prisma migrate dev"
- TypeORM: "Create migration file, define entity with decorators"
- Sequelize: "Define model in models/, create migration"
- Django ORM: "Update models.py, create migration with makemigrations"
- SQLAlchemy: "Define model class, create alembic migration"

---

### Template: `api_crud`

**When to use:** Creating REST API endpoints

**Story structure:**
```json
{
  "id": "[feature]-002",
  "template": "api_crud",
  "title": "Create API endpoints for [Resource]",
  "priority": 2,
  "acceptanceCriteria": [
    "GET /api/[resource] - List all (with pagination, filters)",
    "GET /api/[resource]/:id - Get single",
    "POST /api/[resource] - Create new",
    "PUT /api/[resource]/:id - Update existing",
    "DELETE /api/[resource]/:id - Delete",
    "Request validation using [validator from CODEBASE_ANALYSIS]",
    "Authentication middleware applied",
    "Error handling follows project pattern",
    "Returns consistent response format"
  ],
  "technicalNotes": [
    "Follow route structure: [from CODEBASE_ANALYSIS]",
    "Use [framework] router pattern",
    "Validation schema: [location and library]",
    "Service layer for business logic: [if applicable]",
    "Authorization checks: [pattern from CODEBASE_ANALYSIS]"
  ]
}
```

**Adapt for:**
- Express: "Create router in routes/, controller in controllers/"
- NestJS: "Use @Controller decorator, inject services"
- FastAPI: "Define router with type hints, use Pydantic models"
- Django REST: "Create serializers, viewsets, wire up urls.py"
- Spring Boot: "Create @RestController, @Service classes"

---

### Template: `frontend_component`

**When to use:** Creating UI components

**Story structure:**
```json
{
  "id": "[feature]-003",
  "template": "frontend_component",
  "title": "Create [ComponentName] component",
  "priority": 3,
  "acceptanceCriteria": [
    "Component created in [location from CODEBASE_ANALYSIS]",
    "Props interface defined with TypeScript (if applicable)",
    "Styled using [styling approach from CODEBASE_ANALYSIS]",
    "Responsive design (mobile, tablet, desktop)",
    "Accessible (ARIA labels, keyboard navigation)",
    "State managed using [state approach from CODEBASE_ANALYSIS]",
    "Follows existing component pattern"
  ],
  "technicalNotes": [
    "File naming: [convention from CODEBASE_ANALYSIS]",
    "Import [UI library] components",
    "Use existing hooks: [list common hooks]",
    "Match design system colors/spacing"
  ]
}
```

**Adapt for:**
- React: "Functional component with hooks, TypeScript interface for props"
- Vue: "SFC with Composition API, defineProps with TypeScript"
- Angular: "Component with @Component decorator, template, styles"
- Svelte: "Single-file component with reactive statements"

---

### Template: `frontend_page`

**When to use:** Creating a complete page/route

**Story structure:**
```json
{
  "id": "[feature]-004",
  "template": "frontend_page",
  "title": "Create [PageName] page",
  "priority": 4,
  "acceptanceCriteria": [
    "Page created in [pages directory]",
    "Route added to router configuration",
    "Page includes: [list sections/components]",
    "Data fetching using [data fetching library]",
    "Loading states handled",
    "Error states handled",
    "Empty states handled",
    "SEO metadata (title, description)",
    "Protected route (if authentication required)"
  ],
  "technicalNotes": [
    "Follow routing pattern: [from CODEBASE_ANALYSIS]",
    "Use [data fetching approach] for API calls",
    "Compose with existing components",
    "Match layout structure of similar pages"
  ]
}
```

---

### Template: `form_with_validation`

**When to use:** Creating forms with validation

**Story structure:**
```json
{
  "id": "[feature]-005",
  "template": "form_with_validation",
  "title": "Create [FormName] form",
  "priority": 5,
  "acceptanceCriteria": [
    "Form fields: [list all fields with types]",
    "Validation schema using [validator from CODEBASE_ANALYSIS]",
    "Client-side validation with error messages",
    "Form submission calls API endpoint",
    "Success state with confirmation message",
    "Error handling with user-friendly messages",
    "Disabled state during submission",
    "Field-level validation feedback"
  ],
  "technicalNotes": [
    "Use [form library] from CODEBASE_ANALYSIS",
    "Schema validation: [library and location]",
    "Follow form pattern from existing forms",
    "Toast notifications: [library from CODEBASE_ANALYSIS]"
  ]
}
```

---

### Template: `integration`

**When to use:** Integrating with external services or existing modules

**Story structure:**
```json
{
  "id": "[feature]-006",
  "template": "integration",
  "title": "Integrate with [Service/Module]",
  "priority": 6,
  "acceptanceCriteria": [
    "Integration point identified",
    "API client/service created",
    "Configuration added to env variables",
    "Error handling for service failures",
    "Retry logic (if applicable)",
    "Logging of integration calls",
    "Integration tested with real service"
  ],
  "technicalNotes": [
    "Service location: [where to place integration code]",
    "Follow pattern from existing integrations",
    "Use existing HTTP client: [from CODEBASE_ANALYSIS]",
    "Error handling: [pattern from CODEBASE_ANALYSIS]"
  ]
}
```

---

### Template: `authentication_authorization`

**When to use:** Adding auth-protected features

**Story structure:**
```json
{
  "id": "[feature]-007",
  "template": "authentication_authorization",
  "title": "Add authentication/authorization for [Feature]",
  "priority": 7,
  "acceptanceCriteria": [
    "Authentication middleware applied to routes",
    "Permission checks implemented",
    "Unauthorized access returns 401/403",
    "Frontend shows/hides based on permissions",
    "Token refresh handled (if applicable)",
    "Logout clears authorization state"
  ],
  "technicalNotes": [
    "Follow auth pattern: [from CODEBASE_ANALYSIS]",
    "Use existing middleware: [location]",
    "Permission checking: [how it's done]",
    "Frontend auth state: [how it's managed]"
  ]
}
```

---

### Template: `testing`

**When to use:** Adding tests for features

**Story structure:**
```json
{
  "id": "[feature]-008",
  "template": "testing",
  "title": "Add tests for [Feature]",
  "priority": 8,
  "acceptanceCriteria": [
    "Unit tests for services/utilities",
    "API endpoint tests (if backend)",
    "Component tests (if frontend)",
    "Integration tests for full flow",
    "All tests pass",
    "Coverage meets threshold: [X%]"
  ],
  "technicalNotes": [
    "Test framework: [from CODEBASE_ANALYSIS]",
    "Test file location: [pattern from CODEBASE_ANALYSIS]",
    "Mocking pattern: [how mocks are created]",
    "Follow existing test structure"
  ]
}
```

---

## Story Sizing Guidelines

**Complexity Estimation:**

**Small (1-2 hours):**
- Single file changes
- Add a field to model
- Create a simple component
- Add a single API endpoint
- < 100 lines of code

**Medium (3-6 hours):**
- Multiple related files
- CRUD API endpoints
- Form with validation
- Page with data fetching
- 100-300 lines of code

**Large (1-2 days):**
- Complex feature requiring multiple files
- Integration with external service
- Multi-step flow
- Complex business logic
- > 300 lines of code

**⚠️ If a story is "Large", split it into multiple Medium/Small stories**

---

## Story Ordering Principles

**Dependency-Based Order:**

1. **Database** - Create/update models first (nothing works without data layer)
2. **Backend API** - Create endpoints to manipulate data
3. **Frontend Components** - Build UI elements
4. **Frontend Pages** - Compose components into pages
5. **Integration** - Connect to external services
6. **Testing** - Validate everything works
7. **Documentation** - Document the feature

**Example:**
```
Priority 1: Create Post model
Priority 2: Create Post API endpoints
Priority 3: Create PostCard component
Priority 4: Create PostList component
Priority 5: Create Posts page
Priority 6: Add tests
Priority 7: Update API documentation
```

---

## Acceptance Criteria Rules

**Good Acceptance Criteria:**
- ✅ Specific and measurable
- ✅ Testable (you can verify it's done)
- ✅ Includes technical details
- ✅ References actual file paths/patterns

**Examples:**

✅ **GOOD:**
- "POST /api/users endpoint created in src/routes/users.ts"
- "Returns 201 with user object { id, email, name, createdAt }"
- "Validates email format using Zod schema"
- "Existing tests still pass"

❌ **BAD:**
- "API works"
- "Endpoint created"
- "Validation added"
- "Everything works fine"

---

## Technical Notes Guidelines

**Include:**
- Which files to create/modify
- Which patterns to follow (reference CODEBASE_ANALYSIS.md)
- Which existing code to reference
- Specific libraries/functions to use
- Common gotchas for this type of work

**Example:**
```json
"technicalNotes": [
  "Follow user model pattern from src/models/user.model.ts",
  "Use existing validateEmail() from src/utils/validation.ts",
  "Place route in src/routes/users/ folder",
  "Import auth middleware from src/middleware/auth.ts",
  "Response format must match existing API pattern: { success, data, error }"
]
```

---

## Auto-Adaptation to Tech Stack

**The PRD must adapt to the actual tech stack.**

### Example: Same feature, different stacks

**Feature:** "Create user profile API"

**If React + Express + Prisma:**
```json
{
  "id": "profile-001",
  "title": "Create profile API endpoints",
  "acceptanceCriteria": [
    "Routes in src/routes/profile.routes.ts",
    "Controller in src/controllers/profile.controller.ts",
    "Validation using Zod schema",
    "Prisma queries in service layer"
  ]
}
```

**If Vue + Django + PostgreSQL:**
```json
{
  "id": "profile-001",
  "title": "Create profile API endpoints",
  "acceptanceCriteria": [
    "View created in profiles/views.py",
    "Serializer in profiles/serializers.py",
    "URL pattern in profiles/urls.py",
    "Raw SQL queries in profiles/queries.py"
  ]
}
```

**→ Always check CODEBASE_ANALYSIS.md to generate correct structure!**

---

## Handling Unclear Requirements

**If the feature request is vague:**

1. **Make reasonable assumptions** based on CODEBASE_ANALYSIS.md
2. **Document assumptions** in the `assumptions` array
3. **Ask clarifying questions** in a `clarifications` section

**Example:**
```json
{
  "assumptions": [
    "User can only edit their own profile (based on existing auth pattern)",
    "Profile picture uploads use existing file upload service",
    "Profile changes don't require approval"
  ],
  
  "clarifications": [
    "Should profile changes be logged in audit trail?",
    "Is profile data public or private?",
    "Should we support profile themes/customization?"
  ]
}
```

---

## Quality Checks in Stories

**Every code-producing story should include:**

```json
"acceptanceCriteria": [
  // ... feature criteria ...
  
  // Quality criteria (adapt to project):
  "TypeScript compilation passes (if TS project)",
  "Linting passes with 0 errors",
  "Prettier formatting applied (if used)",
  "Existing tests still pass",
  "New tests added for new functionality (if project has tests)"
]
```

**Check CODEBASE_ANALYSIS.md for:**
- What linter is used
- What test framework is used
- What quality tools exist

---

## Complete PRD Example

```json
{
  "feature": {
    "name": "User Profile Management",
    "description": "Users can view and edit their profile information, upload profile pictures, and change passwords",
    "branch": "feature/user-profile"
  },
  
  "techContext": {
    "frontend": "React 19 with TypeScript, Vite, TanStack Query",
    "backend": "Express with TypeScript, Prisma ORM",
    "database": "PostgreSQL"
  },
  
  "integrationPoints": [
    "Existing User model (extends it)",
    "Existing authentication system (JWT)",
    "File upload service (AWS S3)"
  ],
  
  "stories": [
    {
      "id": "profile-001",
      "template": "database_model",
      "title": "Extend User model with profile fields",
      "description": "Add bio, avatar, phone fields to User model",
      "priority": 1,
      "estimatedComplexity": "small",
      "passes": false,
      "acceptanceCriteria": [
        "Prisma schema updated: User model has bio, avatarUrl, phone fields",
        "Migration created with: prisma migrate dev --name add_profile_fields",
        "Prisma client regenerated",
        "Migration tested locally"
      ],
      "technicalNotes": [
        "Edit prisma/schema.prisma",
        "Follow existing User model field naming (camelCase)",
        "avatarUrl is optional String?",
        "bio is optional String? with @db.Text for long content",
        "phone is optional String?"
      ],
      "filesExpected": [
        "prisma/schema.prisma (modified)",
        "prisma/migrations/XXX_add_profile_fields/ (new)"
      ]
    },
    
    {
      "id": "profile-002",
      "template": "api_crud",
      "title": "Create profile API endpoints",
      "description": "CRUD endpoints for user profile management",
      "priority": 2,
      "estimatedComplexity": "medium",
      "passes": false,
      "acceptanceCriteria": [
        "GET /api/profile - Get current user's profile",
        "PUT /api/profile - Update current user's profile",
        "PATCH /api/profile/avatar - Upload avatar",
        "DELETE /api/profile/avatar - Remove avatar",
        "All endpoints require authentication",
        "Validation using Zod schemas",
        "Returns 401 if not authenticated",
        "Bio max length: 500 characters",
        "Phone validated as E.164 format"
      ],
      "technicalNotes": [
        "Create src/routes/profile.routes.ts",
        "Create src/controllers/profile.controller.ts",
        "Create src/services/profile.service.ts",
        "Use existing auth middleware: src/middleware/auth.ts",
        "Validation schemas in src/validators/profile.validator.ts",
        "File upload: use existing uploadMiddleware from src/middleware/upload.ts",
        "Follow response format: { success: true, data: {...} }"
      ],
      "filesExpected": [
        "src/routes/profile.routes.ts",
        "src/controllers/profile.controller.ts",
        "src/services/profile.service.ts",
        "src/validators/profile.validator.ts"
      ]
    },
    
    {
      "id": "profile-003",
      "template": "frontend_component",
      "title": "Create ProfileForm component",
      "description": "Form for editing profile information",
      "priority": 3,
      "estimatedComplexity": "medium",
      "passes": false,
      "acceptanceCriteria": [
        "Component in src/components/profile/ProfileForm.tsx",
        "Fields: bio (textarea), phone (input), avatar (file upload)",
        "Uses React Hook Form + Zod validation",
        "Validates bio max 500 chars",
        "Validates phone format",
        "Shows character count for bio",
        "Preview avatar before upload",
        "Disabled state during submission",
        "Success toast on save",
        "Error toast on failure",
        "Mobile responsive"
      ],
      "technicalNotes": [
        "Use React Hook Form from existing pattern",
        "Zod schema matches backend validator",
        "Use Radix UI components (from codebase)",
        "Tailwind CSS for styling",
        "Toast: use Sonner from existing setup",
        "Avatar preview: use FileReader API",
        "Follow existing form pattern from src/components/forms/BaseForm.tsx"
      ],
      "filesExpected": [
        "src/components/profile/ProfileForm.tsx",
        "src/components/profile/AvatarUpload.tsx"
      ]
    },
    
    {
      "id": "profile-004",
      "template": "frontend_page",
      "title": "Create Profile page",
      "description": "Main profile management page",
      "priority": 4,
      "estimatedComplexity": "small",
      "passes": false,
      "acceptanceCriteria": [
        "Page in src/pages/Profile.tsx",
        "Route added to router: /profile",
        "Protected route (requires authentication)",
        "Fetches profile data using TanStack Query",
        "Shows ProfileForm component",
        "Loading state while fetching",
        "Error state if fetch fails",
        "Page title: 'My Profile'"
      ],
      "technicalNotes": [
        "Follow page pattern from src/pages/Dashboard.tsx",
        "Use useQuery from @tanstack/react-query",
        "Query key: ['profile', userId]",
        "Protected route: wrap with RequireAuth component",
        "Add route in src/App.tsx"
      ],
      "filesExpected": [
        "src/pages/Profile.tsx",
        "src/App.tsx (modified)"
      ]
    },
    
    {
      "id": "profile-005",
      "template": "testing",
      "title": "Add tests for profile feature",
      "description": "Unit and integration tests",
      "priority": 5,
      "estimatedComplexity": "medium",
      "passes": false,
      "acceptanceCriteria": [
        "API tests: profile.test.ts with all endpoints",
        "Component tests: ProfileForm.test.tsx",
        "Test validation errors",
        "Test successful submission",
        "Test avatar upload",
        "All tests pass",
        "Coverage > 80% for new code"
      ],
      "technicalNotes": [
        "Use Vitest (from existing setup)",
        "API tests in tests/api/profile.test.ts",
        "Component tests use React Testing Library",
        "Mock TanStack Query with createWrapper",
        "Follow test pattern from tests/api/auth.test.ts"
      ],
      "filesExpected": [
        "tests/api/profile.test.ts",
        "tests/components/ProfileForm.test.tsx"
      ]
    }
  ],
  
  "assumptions": [
    "Users can only edit their own profile",
    "Avatar upload uses existing S3 integration",
    "No profile approval workflow needed"
  ],
  
  "outOfScope": [
    "Public profile pages",
    "Social media integration",
    "Profile visibility settings"
  ],
  
  "clarifications": []
}
```

---

## Output Instructions

1. **Read CODEBASE_ANALYSIS.md first** - Don't proceed without it
2. **Generate stories using templates** - Adapt to actual tech stack
3. **Keep stories small** - Split large stories
4. **Order by dependencies** - Database → Backend → Frontend
5. **Be specific** - File paths, function names, patterns
6. **Save to prd.json** - Use exact JSON structure above

---

## After Generation

**Present to user:**

```
✅ PRD Generated: prd.json

📊 Summary:
- Feature: [name]
- Stories: [count]
- Estimated: [X small + Y medium + Z large]
- Tech: [frontend] + [backend] + [database]

📋 Story Breakdown:
1. [story-001]: [title] (Priority: 1, Size: small)
2. [story-002]: [title] (Priority: 2, Size: medium)
...

⚠️ Assumptions Made:
- [assumption 1]
- [assumption 2]

❓ Clarifications Needed (if any):
- [question 1]
- [question 2]

🚀 Next Steps:
1. Review prd.json
2. Edit if needed
3. Run: "Read EXECUTE_STORY.md and execute first story"

Ready to proceed? Say "start execution" or review/edit prd.json first.
```

---

**You are now ready to generate high-quality PRDs that integrate seamlessly with any codebase!**
