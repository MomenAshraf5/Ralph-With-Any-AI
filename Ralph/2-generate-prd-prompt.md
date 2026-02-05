# Antigravity PRD Generator - Step 2: Generate PRD for New Feature

You have already analyzed the codebase (see `CODEBASE_ANALYSIS.md`). Now you will generate a detailed PRD for a new feature that follows the existing project patterns.

## Your Task

Generate a complete PRD in JSON format that:

1. Follows the existing codebase patterns
2. Uses the actual tech stack
3. Breaks the feature into small, focused user stories
4. Includes clear acceptance criteria
5. Respects existing conventions

## Input Format

The user will provide a feature request like:

```
Feature: Overtime Management

Requirements:
- Overtime request submission
- Approval workflow
- Configurable overtime rates (1.5x, 2.0x)
- Automatic calculation from clock-out time
- Overtime history
```

## Output Format

Generate `prd.json` with this structure:

```json
{
  "projectName": "ERP System - [Feature Name]",
  "branchName": "feature/[feature-name-kebab-case]",
  "description": "[Clear description of the feature]",
  "techStack": {
    "frontend": "React 19 with TypeScript, Vite, React Router, TanStack Query, Radix UI, Tailwind CSS",
    "backend": "Node.js with Express, TypeScript, Prisma ORM, PostgreSQL",
    "notes": "[Any specific notes about integration with existing systems]"
  },
  "userStories": [
    {
      "id": "[feature-abbrev]-001",
      "title": "[Clear, action-oriented title]",
      "description": "[Detailed description of what needs to be done]",
      "priority": 1,
      "passes": false,
      "acceptanceCriteria": [
        "[Specific, measurable criterion]",
        "[Another criterion]"
      ],
      "technicalNotes": "[Implementation hints, gotchas, patterns to follow]"
    }
  ],
  "dependencies": ["[List existing systems this integrates with]"],
  "assumptions": ["[List assumptions about existing data/systems]"]
}
```

## Critical Rules for Story Creation

### 1. Small, Focused Stories

Each story should be completable in ONE iteration (single context window).

**Good Story Sizes:**

- ✅ Create database schema for feature
- ✅ Build API endpoint for creating requests
- ✅ Create form component for submission
- ✅ Add approval UI for managers

**Too Large (SPLIT THESE):**

- ❌ Build entire overtime system
- ❌ Implement complete approval workflow (split into: API, UI, notifications)
- ❌ Create all admin screens

### 2. Follow Existing Patterns

Based on `CODEBASE_ANALYSIS.md`, ensure stories use:

**Frontend:**

- Components in correct directory
- React Query for data fetching
- React Hook Form + Zod for forms
- Radix UI components + Tailwind styling
- Proper TypeScript types

**Backend:**

- Prisma models in schema.prisma
- Routes in existing route structure
- Controllers/services pattern
- Zod validation
- JWT auth middleware
- Proper error handling

**Database:**

- Follow Prisma naming conventions
- Use existing relationship patterns
- Proper migrations with `prisma migrate dev`

### 3. Story Ordering

Order stories logically:

1. **Database** - Schema and migrations first
2. **Backend API** - CRUD endpoints
3. **Frontend Components** - UI elements
4. **Integration** - Connect to existing systems
5. **Tests** - Validation
6. **Documentation** - Finish with docs

### 4. Clear Acceptance Criteria

Each criterion should be:

- **Specific**: "POST /api/overtime/requests endpoint created"
- **Measurable**: "Returns 200 status with request object"
- **Testable**: "TypeScript compilation passes with no errors"

**Good Criteria:**

- ✅ "Overtime request form validates hours > 0"
- ✅ "Manager can only approve requests from direct reports"
- ✅ "API returns 403 if user lacks permission"

**Too Vague:**

- ❌ "Form works well"
- ❌ "API is secure"
- ❌ "UI looks good"

### 5. Integration with Existing Systems

**IMPORTANT:** Always check `CODEBASE_ANALYSIS.md` for:

- What systems already exist?
- How to integrate with them?
- What data is already available?

Example:

```json
{
  "id": "overtime-005",
  "title": "Auto-calculate overtime from clock-out",
  "technicalNotes": "Integrate with existing TimeTracking model (see CODEBASE_ANALYSIS.md). Use ClockEntry.clockOut to calculate overtime hours. Trigger on ClockEntry.update event."
}
```

### 6. Include Quality Gates

Every story involving code should have:

- "TypeScript compilation passes (`pnpm build` succeeds)"
- "ESLint shows no errors (`pnpm lint` passes)"
- "Existing tests still pass" (if tests exist)
- "New tests added for [specific functionality]" (for complex logic)

## Example Story Breakdown

**User Request:** "Add overtime approval workflow"

**Your Generated Stories:**

```json
[
  {
    "id": "ot-001",
    "title": "Create overtime_requests table and Prisma model",
    "priority": 1,
    "acceptanceCriteria": [
      "Prisma schema updated with OvertimeRequest model",
      "Migration created and runs successfully",
      "Model has: id, employeeId, date, hours, rate, status, reason, timestamps",
      "Foreign key to Employee model",
      "Status enum: PENDING, APPROVED, REJECTED"
    ],
    "technicalNotes": "Follow existing Prisma model patterns from Employee/Department. Use @prisma/client types. Migration: pnpm prisma:migrate"
  },
  {
    "id": "ot-002",
    "title": "Create POST /api/overtime/requests endpoint",
    "priority": 2,
    "acceptanceCriteria": [
      "Route created in src/routes/overtime.routes.ts",
      "Controller handles request in src/controllers/overtime.controller.ts",
      "Validates: hours > 0, date is past, employee exists (Zod schema)",
      "Returns 201 with created request object",
      "Returns 400 for validation errors",
      "Requires authentication (JWT middleware)"
    ],
    "technicalNotes": "Follow pattern from attendance routes. Use existing auth middleware. Service layer for business logic."
  },
  {
    "id": "ot-003",
    "title": "Create approval endpoint with authorization",
    "priority": 3,
    "acceptanceCriteria": [
      "POST /api/overtime/requests/:id/approve",
      "POST /api/overtime/requests/:id/reject",
      "Checks user is employee's direct manager (via orgChart)",
      "Returns 403 if not authorized",
      "Updates status to APPROVED/REJECTED",
      "Cannot approve own requests"
    ],
    "technicalNotes": "Query Department/OrgChart to verify manager relationship. Add to overtime.service.ts"
  },
  {
    "id": "ot-004",
    "title": "Create overtime request form component",
    "priority": 4,
    "acceptanceCriteria": [
      "Component: src/components/overtime/OvertimeRequestForm.tsx",
      "Uses React Hook Form + Zod schema",
      "Fields: date picker (past only), hours input, rate selector, reason textarea",
      "Uses TanStack Query mutation to submit",
      "Shows success toast on submit (Sonner)",
      "Shows validation errors inline",
      "Radix UI date picker and select components"
    ],
    "technicalNotes": "Follow AttendanceRequestForm pattern. Use existing form components from components/ui/. Match current design system."
  }
]
```

## Questions to Ask Before Generating

If the feature request is unclear, generate the PRD with assumptions documented, but add a `"clarifications_needed"` section:

```json
{
  "clarifications_needed": [
    "Who can submit overtime? All employees or specific roles?",
    "Should there be a limit on overtime hours per day/week?",
    "Are overtime rates per-employee or company-wide?"
  ]
}
```

## How to Run This

1. **Read** `CODEBASE_ANALYSIS.md` thoroughly
2. **Understand** the feature request from user
3. **Generate** complete PRD following all patterns
4. **Review** that stories are small and focused
5. **Save** to `prd.json`
6. **Output** summary and ask user to review before execution

## After Generation

Output to user:

```
✅ PRD Generated: prd.json

📊 Summary:
- [X] user stories created
- Covers: [brief list of what's included]
- Tech: [Frontend] + [Backend] + [Database]
- Estimated: [X stories × ~1 iteration = X iterations total]

❓ Clarifications Needed:
[List any unclear requirements]

📝 Next Steps:
1. Review the PRD in prd.json
2. Edit if needed (add/remove/modify stories)
3. When ready, I'll start executing stories one by one
4. Or say "start execution" to begin immediately

Would you like to review the PRD or should I start execution?
```

## Ready to Generate

When user provides feature requirements, follow this process and generate the PRD!
