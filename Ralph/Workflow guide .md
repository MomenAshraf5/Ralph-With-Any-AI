# Complete Antigravity Ralph Workflow

This guide shows you how to use the three-step process to autonomously develop features in your existing system.

## 📋 Overview

**3-Step Process:**

1. **Analyze** - Antigravity learns your codebase
2. **Generate** - Antigravity creates a PRD for your feature
3. **Execute** - Antigravity implements stories one by one

## 🚀 Initial Setup (One-Time)

### Step 1: Analyze Your Codebase

**What:** Antigravity explores your entire project and documents patterns.

**Command in Antigravity:**

```
Read the file 1-analyze-codebase-prompt.md and follow its instructions to analyze this codebase. Create CODEBASE_ANALYSIS.md with complete documentation.
```

**Output:** `CODEBASE_ANALYSIS.md` (keeps this updated as project evolves)

**When to Re-run:**

- Major architectural changes
- New patterns introduced
- New libraries added
- Every few months to keep fresh

---

## 🎯 For Each New Feature

### Step 2: Generate PRD

**What:** You describe the feature, Antigravity generates a detailed PRD.

**Your Feature Request:**

```
Feature: Overtime Management

Requirements:
- Overtime request submission
- Approval workflow
- Configurable overtime rates (1.5x, 2.0x)
- Automatic calculation from clock-out time
- Overtime history

[Add any other details you want]
```

**Command in Antigravity:**

```
Read 2-generate-prd-prompt.md and CODEBASE_ANALYSIS.md, then generate a PRD for this feature:

[Paste your feature request here]

Save the PRD to prd.json
```

**Antigravity Will:**

1. Read your codebase analysis
2. Generate complete PRD with user stories
3. Ask clarifying questions if needed
4. Save to `prd.json`
5. Show you a summary

**Review the PRD:**

```json
{
  "userStories": [
    {
      "id": "ot-001",
      "title": "Create database schema",
      "priority": 1,
      "passes": false,
      "acceptanceCriteria": [...]
    },
    // ... more stories
  ]
}
```

**You Can:**

- ✅ Accept as-is → Proceed to Step 3
- ✏️ Edit stories (add/remove/modify)
- ❌ Regenerate with more details
- 🔧 Adjust priorities

---

### Step 3: Execute Stories

**What:** Antigravity implements each story, one at a time.

**Command in Antigravity (for EACH story):**

```
Read 3-execute-stories-prompt.md, CODEBASE_ANALYSIS.md, progress.txt, and prd.json.

Execute the next incomplete story from the PRD.
```

**Antigravity Will:**

1. Find next story where `passes: false`
2. Implement it completely
3. Run quality checks
4. Update `prd.json`
5. Document learnings in `progress.txt`
6. Commit changes
7. Show summary
8. **STOP** (waits for you to run next iteration)

**After Each Story:**

1. Review the changes
2. Test if needed
3. Run the command again for next story
4. Repeat until all stories complete

---

## 📁 File Structure After Setup

```
your-project/
├── CODEBASE_ANALYSIS.md           # Project patterns (Step 1)
├── prd.json                       # Current feature PRD (Step 2)
├── progress.txt                   # Learning history (Step 3)
├── 1-analyze-codebase-prompt.md   # Step 1 instructions
├── 2-generate-prd-prompt.md       # Step 2 instructions
├── 3-execute-stories-prompt.md    # Step 3 instructions
├── frontend/
│   └── package.json
├── backend/
│   └── package.json
└── [rest of your project]
```

---

## 🎬 Complete Example Workflow

### Initial Setup

```bash
# 1. Add the prompt files to your project
cp 1-analyze-codebase-prompt.md your-erp/
cp 2-generate-prd-prompt.md your-erp/
cp 3-execute-stories-prompt.md your-erp/

# 2. Open in Antigravity
cd your-erp
# (Open Antigravity IDE)
```

### In Antigravity - First Time

```
You: Read 1-analyze-codebase-prompt.md and analyze this codebase

[Antigravity explores and creates CODEBASE_ANALYSIS.md]

Antigravity: ✅ Analysis complete! CODEBASE_ANALYSIS.md created with:
- Frontend structure (React + Vite + TanStack)
- Backend structure (Express + Prisma)
- Existing features documented
- Code patterns captured
```

### Generate PRD for New Feature

```
You: Read 2-generate-prd-prompt.md and generate PRD for:

Feature: Overtime Management
- Request submission
- Approval workflow
- Configurable rates
- Auto-calculation from clock-out
- History view

[Antigravity generates prd.json]

Antigravity: ✅ PRD Generated!
- 12 user stories
- Covers backend, frontend, database, integration
- Review prd.json and let me know when ready to start
```

### Execute Stories

```
You: Looks good! Read 3-execute-stories-prompt.md and execute the first story

[Antigravity implements story ot-001]

Antigravity: ✅ Story ot-001 Complete!
- Created Prisma models
- Migration successful
- Types generated
- 11 stories remaining

You: Execute next story

[Antigravity implements story ot-002]

Antigravity: ✅ Story ot-002 Complete!
- Created API endpoints
- Added validation
- All checks passed
- 10 stories remaining

You: Execute next story

[Continue for all 12 stories...]

Antigravity: 🎉 All stories complete! Feature ready for testing.
```

---

## 💡 Tips & Best Practices

### For Better PRD Generation

- Be specific in feature requests
- Mention integration points with existing systems
- Note any special requirements upfront
- Reference existing features as examples

### During Execution

- Review each commit before continuing
- Test critical changes as you go
- Don't run all stories blindly - check periodically
- If something looks wrong, stop and fix before continuing

### Maintaining Quality

- Keep CODEBASE_ANALYSIS.md updated
- Review progress.txt periodically
- Update AGENTS.md files with new patterns
- Run full test suite after major features

### When Things Go Wrong

- Check progress.txt for notes
- Review CODEBASE_ANALYSIS.md for patterns
- Story too large? Split it in PRD before execution
- Integration issue? Document in progress.txt

---

## 🔄 Continuous Improvement

As you use this system:

1. **Update CODEBASE_ANALYSIS.md** when:
   - Architecture changes
   - New patterns emerge
   - New libraries added

2. **Improve PRD Templates** by noting:
   - What story sizes work best
   - What criteria are clearest
   - What technical notes help most

3. **Refine Prompts** based on:
   - Common mistakes Antigravity makes
   - Patterns that work well
   - Edge cases encountered

---

## 📊 Tracking Progress

### Check Story Status

```bash
# In your project
cat prd.json | grep -A 2 '"id"'
```

### View Learning History

```bash
cat progress.txt
```

### Check Recent Commits

```bash
git log --oneline -10
```

---

## 🆘 Troubleshooting

### "Antigravity can't find the pattern"

→ Update CODEBASE_ANALYSIS.md with the pattern

### "Story is taking too long"

→ Story is too large, split it in prd.json

### "Quality checks failing"

→ Fix manually, document in progress.txt, continue

### "Generated code doesn't match style"

→ Document exact patterns in CODEBASE_ANALYSIS.md

### "PRD missing important details"

→ Provide more specific feature requirements

---

## ✅ Success Checklist

Before starting execution:

- [ ] CODEBASE_ANALYSIS.md exists and is current
- [ ] prd.json reviewed and approved
- [ ] progress.txt initialized
- [ ] All three prompt files in project
- [ ] Git working directory is clean

During execution:

- [ ] Review each commit
- [ ] Quality checks passing
- [ ] progress.txt being updated
- [ ] prd.json marking stories complete

After feature complete:

- [ ] All stories marked `passes: true`
- [ ] Manual testing performed
- [ ] Documentation updated
- [ ] CODEBASE_ANALYSIS.md updated if needed

---

## 🎓 Learning Outcomes

After using this workflow, you'll have:

1. **Documented codebase** - CODEBASE_ANALYSIS.md serves as living documentation
2. **Consistent patterns** - New code follows existing conventions
3. **Learning history** - progress.txt captures institutional knowledge
4. **Autonomous development** - Features built while you focus on high-level decisions
5. **Quality assurance** - Built-in checks prevent technical debt

---

## 🚀 Ready to Start!

1. Copy the three prompt files to your project
2. Run Step 1 (Analyze Codebase) once
3. For each feature: Run Step 2 (Generate PRD) → Review → Run Step 3 (Execute)
4. Watch your system grow autonomously!

**Questions?**

- Check CODEBASE_ANALYSIS.md for patterns
- Review progress.txt for learnings
- Examine prd.json for story details
