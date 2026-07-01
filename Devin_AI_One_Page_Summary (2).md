
# 🔥 DEVIN AI: THE ONE-PAGE POWER SUMMARY
## Print This. Tape It To Your Monitor.

---

## 💰 THE ACU EQUATION
```
1 ACU = ~15 min work = $2.00-$2.25
Well-scoped task = 1-3 ACUs ($2-7)
Poorly scoped task = 5-15+ ACUs ($10-34)
Savings from playbooks = 30-50% after 3rd iteration
Savings from parallel Devins = 25-40% on multi-file tasks
```

## 🎯 THE 5 COMMANDMENTS OF ACU OPTIMIZATION

### 1. WORK-ORDER PROMPT (Saves 40-60% ACUs)
```
GOAL: [One sentence]
CONTEXT: [Repo, branch, stack, reference files]
ACCEPTANCE CRITERIA: [Numbered, verifiable, with commands]
SCOPE: [In scope + Out of scope — BE EXPLICIT]
ENVIRONMENT HINTS: [Install, test, lint commands]
CLOSING STEP: [PR title, branch, stop condition]
```

### 2. SET ACU LIMITS (Prevents runaway sessions)
| Task Type | Limit |
|-----------|-------|
| Bug fix | 3-5 ACUs |
| Feature | 8-10 ACUs |
| Migration | 15-20 ACUs |
| Research | 5 ACUs |

### 3. USE CHECKPOINTS (Saves 25-40%)
```
"Plan the DB schema → STOP → I approve → Implement backend → STOP → 
I approve → Implement frontend → STOP → Done"
```

### 4. BUILD SNAPSHOTS (Saves 1-2 ACUs per session)
- Pre-install dependencies
- Pre-configure secrets
- Pre-clone repos
- One-time setup, forever savings

### 5. ATOMIC KNOWLEDGE (Saves token burn)
```
❌ One 5,000-word doc (loaded every session)
✅ 15-20 focused items <500 words (loaded when triggered)
```

---

## 🤖 HIDDEN FEATURES MOST TEAMS DON'T USE

| Feature | What It Does | ACU Impact |
|---------|-------------|------------|
| **Managed Devins** | One coordinator spawns parallel child sessions | -25-40% on multi-file tasks |
| **Playbook Macros** | `!add-endpoint` loads full template instantly | -30-50% per task |
| **Session Insights** | Post-session analysis with actionable feedback | Prevents repeat mistakes |
| **Preview Agent** | Faster execution, streaming thoughts | -10-15% per session |
| **Devin Review** | AI-powered PR review with security findings | Catches bugs before merge |
| **Scheduled Sessions** | Automated maintenance (tests, docs, deps) | Runs while you sleep |
| **CLI Handoff** | Local exploration → `/handoff` → cloud execution | Free local + paid cloud only when needed |
| **Duplicate Sessions** | Run 2-3 approaches, pick the best | Higher success rate |
| **Focus Mode** | Cmd+Shift+F — distraction-free | Faster context switching |
| **Agents Tab** | Monitor all child sessions in one view | Better parallel management |

---

## 📋 THE PERFECT PLAYBOOK TEMPLATE

```markdown
# Playbook: [Task Name]

## Procedure
1. [Step 1]
2. [Step 2]
3. [Step 3: Test command]
4. [Step 4: Open PR]

## Specifications
- [What must be true after completion]

## Advice
- [Correct Devin's defaults — your team's patterns]

## Forbidden Actions
- [What Devin must NEVER do]

## Required from User
- [What you need to provide before starting]
```

**Assign a macro:** `!your-macro-name`

---

## 🔧 FILES TO CREATE IN EVERY REPO

```
AGENTS.md              → Project rules (auto-read by Devin CLI)
.devin/config.yaml     → Custom tools and commands
.github/PULL_REQUEST_TEMPLATE/devin_pr_template.md  → PR template
SECURITY.md            → Custom security policies for Devin Review
```

---

## ⚡ THE 30-DAY TRANSFORMATION CHECKLIST

**Week 1:** ☐ Audit ACUs ☐ Create 3-5 Knowledge items ☐ Set up snapshots ☐ Set ACU limits
**Week 2:** ☐ Create 3 playbooks with macros ☐ Test and refine ☐ Measure ACU consumption
**Week 3:** ☐ Run first parallel Devin task ☐ Compare vs. sequential ☐ Document pattern
**Week 4:** ☐ Set up 2-3 scheduled sessions ☐ Enable Slack pipeline ☐ Target 40-50% ACU reduction

---

## 🚨 THE 10 ANTI-PATTERNS THAT BURN ACUs

1. ❌ "Fix the bug" → ✅ Work-Order Prompting
2. ❌ No ACU limits → ✅ 5-10 default limit
3. ❌ Giant Knowledge doc → ✅ Atomic items
4. ❌ No snapshot → ✅ Pre-built environment
5. ❌ Stuck session grinding → ✅ Stop and redirect
6. ❌ Skip plan review → ✅ Always review first
7. ❌ No out-of-scope list → ✅ Explicit forbidden files
8. ❌ Secrets in prompts → ✅ Secrets dashboard
9. ❌ No acceptance criteria → ✅ Verifiable success
10. ❌ Ignore Session Insights → ✅ Review every session

---

## 💡 THE GOLDEN RULE

> "Devin replaces TASKS, not ROLES. The teams that win invest in setup 
> (Knowledge, snapshots, playbooks) BEFORE burning ACUs."

**Expected Result: 40-60% ACU reduction in 30 days.**

---

*Print this. Share it. Live by it.*
