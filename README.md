# RALPH_GUIDE.md

**Ralph: Autonomous Development System for Any Codebase**

Ralph helps you implement features autonomously by:

1. **Analyzing** your codebase to understand patterns
2. **Generating** structured PRDs (Product Requirements Documents)
3. **Executing** stories one-by-one following your conventions

---

## Quick Start

### First Time Setup (5 minutes)

**1. Copy Ralph files to your project:**

```bash
# Copy these 3 core files in Ralph folder
ANALYZE_CODEBASE.md
GENERATE_PRD.md
EXECUTE_STORY.md
```

**2. Analyze your codebase (ONE TIME):**

```
In Antigravity (or your AI agent):
"Read ANALYZE_CODEBASE.md and analyze this codebase"
```

**Output:** `CODEBASE_ANALYSIS.md` - Complete documentation of your project

**3. You're ready!** Now you can generate PRDs and execute stories.

---

## Workflow

### For Each New Feature:

#### Step 1: Generate PRD

```
In Antigravity:
"Read GENERATE_PRD.md and create a PRD for:

Feature: [Your feature name]
Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]
"
```

**Output:** `prd.json` with user stories

**Review the PRD:**

- Check stories make sense
- Edit if needed (add/remove/modify stories)
- Adjust priorities
- Split large stories

#### Step 2: Execute Stories (One at a Time)

```
In Antigravity:
"Read EXECUTE_STORY.md and execute the next story"
```

**What happens:**

1. ✅ Finds next incomplete story
2. ✅ Implements following your patterns
3. ✅ Runs quality checks
4. ✅ Updates PRD
5. ✅ Documents learnings
6. ✅ Commits changes
7. ✅ Reports completion
8. ✅ STOPS (waits for you)

**Repeat** until all stories complete.

---

## File Structure

```
your-project/
├── CODEBASE_ANALYSIS.md    # Your project patterns (generated once)
├── prd.json                # Current feature stories (per feature)
├── progress.txt            # Learning history (append-only)
├── ANALYZE_CODEBASE.md     # Analysis instructions
├── GENERATE_PRD.md         # PRD generation instructions
├── EXECUTE_STORY.md        # Story execution instructions
├── RALPH_GUIDE.md          # This guide
└── [your source code...]
```

---

## Example: Complete Feature Implementation

### Scenario: Add user profile feature

**1. Generate PRD:**

```
In Antigravity:
"Read GENERATE_PRD.md and create PRD for:

Feature: User Profile Management
Requirements:
- Users can view their profile
- Users can edit bio, phone, avatar
- Form validation
- Profile page with route
"
```

**Antigravity generates:** `prd.json` with 5 stories:

- profile-001: Extend User model
- profile-002: Create API endpoints
- profile-003: Create ProfileForm component
- profile-004: Create Profile page
- profile-005: Add tests

**2. Execute stories:**

```
You: "Execute next story"

[Antigravity implements profile-001: Extends User model]
[Updates Prisma schema, runs migration, generates client]
[Commits with message: "feat(profile-001): Extend User model"]

Antigravity: "✅ Story profile-001 complete! 4 stories remaining."

You: "Execute next story"

[Antigravity implements profile-002: Creates API endpoints]
[Creates routes, controllers, validators]
[Runs type check, linting, tests]
[Commits]

Antigravity: "✅ Story profile-002 complete! 3 stories remaining."

[Repeat for remaining stories...]

Antigravity: "🎉 All 5 stories complete! Feature ready."
```

**Result:** Complete profile feature implemented following your exact patterns!

---

## Key Features

### 🔍 Auto-Detection

- Detects your tech stack from package.json, requirements.txt, etc.
- Finds your code patterns automatically
- Adapts to ANY framework (React, Vue, Django, Spring Boot, etc.)

### 📋 Smart Story Templates

- CRUD APIs
- Frontend components
- Database models
- Forms with validation
- Authentication
- Testing
- [More templates in GENERATE_PRD.md]

### ✅ Quality Assurance

- Auto-runs type checking (if TypeScript/Python with types)
- Auto-runs linting (if ESLint/Flake8/etc configured)
- Auto-runs tests (if Jest/Vitest/pytest/etc exists)
- Ensures migrations work (Prisma/Django/Alembic/etc)

### 🚨 Error Handling

- Tries to fix errors automatically (formatting, imports)
- Documents what it cannot fix
- Never breaks existing functionality
- Stops if blocked (doesn't continue blindly)

### 📝 Learning System

- Builds institutional knowledge in progress.txt
- Each story documents learnings
- Future stories benefit from past discoveries

---

## Best Practices

### ✅ DO:

**Review PRDs before execution:**

- Check stories are small enough
- Verify they're in correct order
- Adjust to your needs

**Review each story after completion:**

- Check the code quality
- Test critical features manually
- Verify patterns are correct

**Keep CODEBASE_ANALYSIS.md updated:**

- Re-run analysis after major changes
- Update manually if patterns change
- Treat it as living documentation

**Read progress.txt regularly:**

- See what was learned
- Check for repeated issues
- Use insights for future PRDs

### ❌ DON'T:

**Don't run all stories blindly:**

- Review after each story
- Catch issues early
- Course-correct as needed

**Don't skip quality checks:**

- Quality checks prevent technical debt
- Fix errors immediately
- Don't continue with failing tests

**Don't ignore blockers:**

- If story is blocked, investigate
- Don't just skip to next story
- Fix the root cause

**Don't modify passing tests to make them pass:**

- Tests are your safety net
- Failing tests = broken functionality
- Fix the code, not the tests

---

## Troubleshooting

### Problem: "CODEBASE_ANALYSIS.md not found"

**Solution:**

```
Run: "Read ANALYZE_CODEBASE.md and analyze this codebase"
```

### Problem: "PRD stories are too large"

**Solution:**

- Edit prd.json
- Split large stories into smaller ones
- Each story should be < 300 lines of code

### Problem: "Story failed quality checks"

**Solution:**

- Check error message
- Fix the issue
- Re-run the story

### Problem: "Pattern doesn't match my code"

**Solution:**

- Update CODEBASE_ANALYSIS.md with correct pattern
- Re-generate PRD or manually edit technical notes
- Future stories will use updated pattern

### Problem: "Story is blocked/can't be completed"

**Solution:**

- Check progress.txt for details
- Address the blocking issue
- May need manual intervention
- Then continue

---

## Advanced Usage

### Custom Story Templates

Edit `GENERATE_PRD.md` to add your own templates:

```json
{
  "template": "my_custom_template",
  "title": "...",
  "acceptanceCriteria": [...]
}
```

### Multi-Project Support

Keep separate CODEBASE_ANALYSIS.md for each project:

```
project-a/
├── CODEBASE_ANALYSIS.md
├── [Ralph files]
└── [code]

project-b/
├── CODEBASE_ANALYSIS.md
├── [Ralph files]
└── [code]
```

### Team Collaboration

**Commit Ralph files to Git:**

- Entire team benefits from analysis
- PRDs serve as documentation
- progress.txt is shared knowledge

---

## Supported Tech Stacks

Ralph works with **ANY** codebase. Examples:

### Frontend

- React, Vue, Angular, Svelte, Solid
- Next.js, Nuxt, SvelteKit, Remix
- TypeScript, JavaScript

### Backend

- Node.js (Express, NestJS, Fastify, Koa)
- Python (Django, Flask, FastAPI)
- Java (Spring Boot, Jakarta EE)
- Go (Gin, Echo, Chi)
- PHP (Laravel, Symfony)
- Ruby (Rails, Sinatra)

### Database

- PostgreSQL, MySQL, MongoDB
- Prisma, TypeORM, Sequelize
- Django ORM, SQLAlchemy
- Hibernate, JPA

**If your stack isn't listed:** Ralph will auto-detect it from your dependency files!

---

## FAQ

**Q: Do I need to use Antigravity?**
A: No! Any AI agent can use Ralph. Claude, ChatGPT, local models, etc.

**Q: Can I use Ralph for existing projects?**
A: Yes! Ralph is designed for existing codebases. It analyzes and adapts.

**Q: What if I don't have tests?**
A: No problem. Ralph will skip test-related quality checks if tests don't exist.

**Q: Can I edit the PRD after generation?**
A: Absolutely! PRDs are meant to be reviewed and edited before execution.

**Q: What if a story fails?**
A: Ralph will document the issue in progress.txt and stop. You can investigate and fix, then continue.

**Q: How does Ralph learn?**
A: Through progress.txt. Each story appends learnings that future stories reference.

**Q: Can I add my own quality checks?**
A: Yes! Edit EXECUTE_STORY.md to add custom checks for your project.

**Q: Does Ralph replace developers?**
A: No! Ralph is a tool to speed up implementation. You still review, test, and make decisions.

---

## Getting Help

**If something doesn't work:**

1. Check `progress.txt` for error details
2. Review `CODEBASE_ANALYSIS.md` for correct patterns
3. Verify `prd.json` stories are well-formed
4. Check this guide's troubleshooting section

**Common issues:**

- Re-run analysis if codebase changed significantly
- Split large stories into smaller ones
- Ensure quality checks are properly configured
- Verify environment variables are set

---

## Version & Updates

**Current Version:** 2.0 (Universal Auto-Detect)

**Changelog:**

- v2.0: Auto-detection, story templates, error handling
- v1.0: Initial version (tech-specific)

**To update Ralph:**
Replace the 3 core .md files with latest versions.
Your CODEBASE_ANALYSIS.md and progress.txt are preserved.

---

**Happy Autonomous Coding! 🚀**

Ralph helps you ship features faster while maintaining quality and consistency.
