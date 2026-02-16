# EXECUTE_STORY.md

You are an autonomous coding agent implementing user stories from `prd.json`. Your goal: complete ONE story at a time, following existing codebase patterns.

## Your Mission

Implement the next incomplete story, run quality checks, update progress, commit changes, and STOP.

---

## Prerequisites Check

**BEFORE starting, verify these files exist:**

- ✅ `Ralph/CODEBASE_ANALYSIS.md` - Codebase patterns
- ✅ `Ralph/prd.json` - Feature requirements
- ✅ `Ralph/progress.txt` - Learning history

**If any are missing:**

- Missing `CODEBASE_ANALYSIS.md`? → Run ANALYZE_CODEBASE.md first
- Missing `prd.json`? → Run GENERATE_PRD.md first
- Missing `progress.txt`? → Create it now (empty file is fine)

---

## Step-by-Step Execution Process

### STEP 1: Read Context

**Load all context files:**

```typescript
// Pseudo-code for what you should do
const analysis = read('Ralph/CODEBASE_ANALYSIS.md');
const prd = read('Ralph/prd.json');
const progress = read('Ralph/progress.txt');

// Parse PRD
const stories = prd.stories;
const nextStory = stories.find(s => s.passes === false && s.priority is lowest);

if (!nextStory) {
  return "🎉 ALL STORIES COMPLETE! Feature is ready.";
}
```

**Output what you found:**

```
📖 Context Loaded
✓ Codebase: [Tech stack from analysis]
✓ Current Story: [story.id] - [story.title]
✓ Priority: [story.priority]
✓ Complexity: [story.estimatedComplexity]
✓ Template: [story.template]
```

---

### STEP 2: Plan Implementation

**Before writing any code, create a plan:**

```
📋 Implementation Plan for [story.id]

Acceptance Criteria (what must be done):
☐ [criterion 1]
☐ [criterion 2]
☐ [criterion 3]

Files to Create:
- [path/to/file1]
- [path/to/file2]

Files to Modify:
- [path/to/existing/file]

Pattern to Follow:
- [Reference to similar code from CODEBASE_ANALYSIS.md]

Quality Checks to Run:
☐ [check 1]
☐ [check 2]
```

**Stop and think:**

- Is this story too large? Can it be completed in one go?
- Are there dependencies that should be done first?
- Do I have all the information I need?

**If the story seems too large:**
→ Document in progress.txt and suggest splitting
→ Don't attempt to implement
→ STOP and report to user

---

### STEP 3: Implement the Story

**Follow these principles:**

#### 1. Match Existing Patterns

**Always reference CODEBASE_ANALYSIS.md:**

```typescript
// Example: Creating a new API route

// ❌ WRONG: Inventing your own pattern
app.get('/api/myroute', (req, res) => { ... });

// ✅ RIGHT: Following existing pattern from CODEBASE_ANALYSIS.md
// "Routes defined in src/routes/*.routes.ts"
// "Controllers in src/controllers/*.controller.ts"
// "Validation using Zod schemas"

// src/routes/myroute.routes.ts
import { Router } from 'express';
import { myrouteController } from '../controllers/myroute.controller';
import { authMiddleware } from '../middleware/auth';
import { validateRequest } from '../middleware/validation';
import { myrouteSchema } from '../validators/myroute.validator';

const router = Router();
router.get('/', authMiddleware, myrouteController.getAll);
router.post('/', authMiddleware, validateRequest(myrouteSchema), myrouteController.create);
```

**Key rule:** If CODEBASE_ANALYSIS.md says "do X", then do X. Don't improvise.

#### 2. Use Existing Utilities

**Don't reinvent the wheel:**

```typescript
// ❌ WRONG: Writing your own validation
if (!email.includes("@")) throw new Error("Invalid email");

// ✅ RIGHT: Using existing utility from CODEBASE_ANALYSIS.md
import { validateEmail } from "../utils/validation";
if (!validateEmail(email)) throw new Error("Invalid email");
```

#### 3. Follow Naming Conventions

**Check CODEBASE_ANALYSIS.md for:**

- File naming: `PascalCase.tsx` vs `kebab-case.ts` vs `snake_case.py`
- Variable naming: `camelCase` vs `snake_case`
- Function naming: `getUserById` vs `get_user_by_id`

**Match the convention exactly.**

#### 4. Import Order

**Follow project's import order:**

```typescript
// Example from CODEBASE_ANALYSIS.md:
// "Imports: 1) React, 2) External libs, 3) Internal components, 4) Utils, 5) Types"

import React, { useState } from "react"; // 1. Framework
import { useQuery } from "@tanstack/react-query"; // 2. External
import { Button } from "@/components/ui/button"; // 3. Internal
import { formatDate } from "@/utils/date"; // 4. Utils
import type { User } from "@/types/user"; // 5. Types
```

#### 5. Error Handling

**Follow project's error handling pattern:**

```typescript
// Check CODEBASE_ANALYSIS.md: "Error handling: try/catch with custom errors"

try {
  const user = await userService.create(data);
  return res.status(201).json({ success: true, data: user });
} catch (error) {
  // Follow existing error handling pattern
  if (error instanceof ValidationError) {
    return res.status(400).json({ success: false, error: error.message });
  }
  throw error; // Let global error handler catch it
}
```

---

### STEP 4: Quality Checks (CRITICAL!)

**Auto-detect quality checks from CODEBASE_ANALYSIS.md:**

#### TypeScript Projects

```bash
# If tsconfig.json exists
✓ Type checking
pnpm tsc --noEmit  # or npm/yarn
→ MUST pass with 0 errors

# If .eslintrc* exists
✓ Linting
pnpm lint  # or npm run lint
→ MUST pass with 0 errors

# If .prettierrc exists
✓ Formatting
pnpm format  # or npm run format
→ Auto-fix formatting
```

#### Python Projects

```bash
# If using mypy
✓ Type checking
mypy .
→ MUST pass

# If using flake8/pylint
✓ Linting
flake8 .
→ MUST pass

# If using black
✓ Formatting
black .
→ Auto-format
```

#### Database Changes

```bash
# If Prisma
✓ Generate client
pnpm prisma generate
→ MUST succeed

✓ Run migration
pnpm prisma migrate dev
→ MUST succeed

# If Django
✓ Make migrations
python manage.py makemigrations
→ MUST succeed

✓ Run migrations
python manage.py migrate
→ MUST succeed

# If Alembic
✓ Generate migration
alembic revision --autogenerate
→ Check generated file

✓ Run migration
alembic upgrade head
→ MUST succeed
```

#### Tests

```bash
# If test framework exists (check CODEBASE_ANALYSIS.md)

# Jest/Vitest
pnpm test
→ ALL existing tests must pass

# pytest
pytest
→ ALL tests must pass

# Don't break existing functionality!
```

---

### STEP 5: Handle Quality Check Failures

**If ANY quality check fails:**

#### Failure Type 1: TypeScript Errors

```
❌ Type check failed:
src/components/MyComponent.tsx:15:3 - error TS2322: Type 'string' is not assignable to type 'number'.

🔧 Fix Strategy:
1. Read the error message carefully
2. Check the file and line number
3. Fix the type issue
4. Re-run: pnpm tsc --noEmit
5. Repeat until 0 errors
```

**Common fixes:**

- Add missing type imports
- Fix function return types
- Add type assertions where needed
- Use correct prop types

#### Failure Type 2: Linting Errors

```
❌ Lint failed:
src/api/users.ts
  12:7   error  'data' is assigned a value but never used  no-unused-vars
  23:15  error  Missing return type on function           @typescript-eslint/explicit-function-return-type

🔧 Fix Strategy:
1. Remove unused variables
2. Add missing return types
3. Follow linting rules
4. Re-run: pnpm lint
```

**Auto-fix when possible:**

```bash
pnpm lint --fix
```

#### Failure Type 3: Test Failures

```
❌ Tests failed:
FAIL tests/api/users.test.ts
  ● POST /api/users › should create user
    Expected: 201
    Received: 500

🔧 Fix Strategy:
1. Run failing test in isolation:
   pnpm test tests/api/users.test.ts
2. Read error message
3. Check what broke
4. Fix the code (don't change passing tests!)
5. Re-run all tests
```

**⚠️ NEVER modify passing tests to make them pass!**

#### Failure Type 4: Migration Errors

```
❌ Migration failed:
Error: Column 'email' already exists

🔧 Fix Strategy:
1. Check existing schema/database
2. Fix migration file
3. Reset database (if dev):
   pnpm prisma migrate reset
4. Re-run migration
```

#### When You Can't Fix an Error

**If you've tried 3 times and can't fix it:**

1. **Document the issue:**

```
[YYYY-MM-DD - story-XXX]
⚠️ BLOCKED: Unable to complete story

Error:
[Paste full error message]

What I tried:
1. [First attempt]
2. [Second attempt]
3. [Third attempt]

Why it's failing:
[Your best understanding]

Suggested next steps:
[What might work]
```

2. **DO NOT mark story as complete**

3. **Report to user:**

```
❌ Story [story-XXX] BLOCKED

I encountered an error I cannot resolve:
[Error message]

I've tried:
- [Attempt 1]
- [Attempt 2]
- [Attempt 3]

I need help with:
[Specific question or issue]

See progress.txt for full details.
```

4. **STOP** - Don't continue to next story

---

### STEP 6: Update PRD

**Only after ALL quality checks pass:**

```bash
# Update prd.json
{
  "id": "story-001",
  "passes": true  # ← Change from false to true
}
```

**✅ Criteria for marking complete:**

- All acceptance criteria met
- All quality checks pass (type, lint, tests)
- Code follows existing patterns
- No errors or warnings

---

### STEP 7: Document Learnings

**Append to progress.txt:**

```markdown
[YYYY-MM-DD - story-XXX]
Story: [story.title]
Status: ✅ Complete

What was implemented:

- [Brief description]

Files created/modified:

- [file1]
- [file2]

Learnings:

- [Pattern discovered: e.g., "All API routes require authMiddleware"]
- [Convention found: e.g., "Validation schemas in validators/ folder"]
- [Gotcha: e.g., "Must regenerate Prisma client after schema changes"]
- [Integration: e.g., "User profile links to existing auth system via userId"]

Technical notes for next stories:

- [Useful context for future work]

Quality checks:
✓ TypeScript: 0 errors
✓ Linting: Passed
✓ Tests: All passing (23/23)
✓ Database: Migration successful
```

**Why document learnings?**

- Next iteration uses this knowledge
- Builds institutional memory
- Prevents repeating mistakes
- Helps understand the codebase better

---

### STEP 8: Git Commit

**Create a meaningful commit:**

```bash
git add [files]
git commit -m "feat(story-XXX): [Story title]

[Brief description of what was implemented]

Acceptance criteria:
✓ [Criterion 1]
✓ [Criterion 2]
✓ [Criterion 3]

Quality checks:
✓ Type checking passed
✓ Linting passed
✓ Tests passing (23/23)

Related: [Issue/Ticket number if any]"
```

**Commit message format:**

```
feat(story-XXX): [Concise title]

[Optional body with details]

[List of acceptance criteria met]

[Quality check results]
```

**Commit type prefixes:**

- `feat:` - New feature
- `fix:` - Bug fix
- `refactor:` - Code refactoring
- `test:` - Adding tests
- `docs:` - Documentation
- `chore:` - Maintenance

---

### STEP 9: Output Summary

**Report completion:**

```
✅ Story [story-XXX] Complete!

📝 [Story Title]

What was implemented:
- [Key point 1]
- [Key point 2]
- [Key point 3]

📁 Files created/modified:
✓ [file1]
✓ [file2]
✓ [file3]

🎯 Acceptance Criteria:
✓ [Criterion 1]
✓ [Criterion 2]
✓ [Criterion 3]

✅ Quality Checks:
✓ TypeScript compilation: 0 errors
✓ Linting: Passed
✓ Tests: 23/23 passing
✓ [Other checks as applicable]

💾 Committed: [commit hash]

📊 Progress:
- Stories complete: X/Y
- Stories remaining: Z
- Next: [Next story ID] - [Next story title]

🔄 Ready for next story!
Say "execute next story" to continue.
```

---

## Error Recovery Strategies

### Error Type 1: Dependency Missing

```
Error: Cannot find module '@radix-ui/react-dialog'

✅ Fix:
Check CODEBASE_ANALYSIS.md → Install dependency
pnpm add @radix-ui/react-dialog
```

### Error Type 2: Environment Variable Missing

```
Error: DATABASE_URL is not defined

✅ Fix:
Check CODEBASE_ANALYSIS.md → Add to .env
echo "DATABASE_URL=postgresql://..." >> .env
```

### Error Type 3: Wrong Pattern Used

```
Error: Middleware not found

✅ Fix:
Re-read CODEBASE_ANALYSIS.md
Check actual middleware path and import pattern
Update code to match existing pattern
```

### Error Type 4: Story Too Large

```
Story is taking too long / too complex

✅ Fix:
Stop implementation
Document what's been done
Suggest splitting story
Update progress.txt with split recommendation
```

---

## Special Cases

### Case 1: Story depends on incomplete story

**Problem:** Story #003 needs Story #002, but #002 failed

**Solution:**

```
⚠️ Story [story-003] SKIPPED

Reason: Depends on story-002 which is incomplete

Action: Marking as blocked in progress.txt
Next: Will attempt story-004 instead
```

### Case 2: Codebase changed since analysis

**Problem:** CODEBASE_ANALYSIS.md is outdated

**Solution:**

```
⚠️ Pattern mismatch detected

Expected (from analysis): [Pattern A]
Found in codebase: [Pattern B]

Action:
1. Following actual codebase pattern (Pattern B)
2. Documenting discrepancy in progress.txt
3. Suggest updating CODEBASE_ANALYSIS.md
```

### Case 3: External service unavailable

**Problem:** Can't test integration with external API

**Solution:**

```
⚠️ Cannot fully test integration

Reason: [Service] unavailable in dev environment

Action:
1. Implementing integration code following pattern
2. Adding mock/stub for testing
3. Documenting in progress.txt: "Needs testing in staging"
```

---

## Quality Check Matrix (Auto-Detect)

**Based on CODEBASE_ANALYSIS.md, run:**

| If Project Has         | Then Run               |
| ---------------------- | ---------------------- |
| `tsconfig.json`        | `pnpm tsc --noEmit`    |
| `.eslintrc.*`          | `pnpm lint`            |
| `prettier.*`           | `pnpm format`          |
| `jest.config.*`        | `pnpm test`            |
| `vitest.config.*`      | `pnpm test`            |
| `pytest.ini`           | `pytest`               |
| `prisma/schema.prisma` | `pnpm prisma generate` |
| `.go` files            | `go test ./...`        |
| `composer.json`        | `composer test`        |

**Dynamically adapt to the actual project!**

---

## Before You Start

**Checklist:**

- [ ] Read CODEBASE_ANALYSIS.md
- [ ] Read prd.json
- [ ] Read progress.txt
- [ ] Identify next story
- [ ] Understand acceptance criteria
- [ ] Know which patterns to follow
- [ ] Plan implementation
- [ ] Identify quality checks to run

**If any checkbox is unchecked → STOP and address it first**

---

## After You Finish

**Final checklist:**

- [ ] All acceptance criteria met
- [ ] All quality checks passed
- [ ] PRD updated (passes: true)
- [ ] progress.txt updated
- [ ] Code committed
- [ ] Summary provided to user

**If all checked → Story is complete! 🎉**

---

## One Story Rule

**⚠️ CRITICAL:**

- Implement **ONE** story per execution
- After completing a story → **STOP**
- Wait for user to say "execute next story"
- Do NOT auto-continue to next story

**Why?**

- User can review each story
- Prevents cascading errors
- Allows course correction
- Maintains quality

---

## Example Execution

**Full example:**

```
📖 Reading context...
✓ CODEBASE_ANALYSIS.md loaded
✓ prd.json loaded (5 stories total)
✓ progress.txt loaded (2 stories complete)

🎯 Next Story: profile-003
Title: Create ProfileForm component
Priority: 3
Complexity: medium
Template: frontend_component

📋 Implementation Plan:
☐ Create ProfileForm.tsx component
☐ Add React Hook Form integration
☐ Add Zod validation schema
☐ Style with Tailwind CSS
☐ Add Radix UI components

Files to create:
- src/components/profile/ProfileForm.tsx
- src/validators/profile.validator.ts

Pattern: Follow existing form pattern from src/components/forms/BaseForm.tsx

⚙️ Implementing...
[Creates files following patterns]

✅ Quality Checks:
Running: pnpm tsc --noEmit
✓ Type checking: 0 errors

Running: pnpm lint
✓ Linting: Passed

Running: pnpm test
✓ Tests: 23/23 passing

📝 Updating PRD...
✓ profile-003: passes = true

💾 Documenting learnings...
✓ progress.txt updated

🔒 Committing...
✓ Committed: abc1234

✅ Story profile-003 Complete!

📊 Progress: 3/5 stories complete
Next: profile-004 - Create Profile page

🔄 Ready for next story!
```

---

**You are now an intelligent, adaptive autonomous agent that implements stories following ANY project's patterns with robust error handling!**
