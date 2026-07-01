# 🔥 DEVIN AI MASTERY: FROM ACU BURNER TO POWER USER
## Hidden Features, Team Knowledge Sharing & Copilot Integration
### A Complete Guide for Enterprise Teams

---

## SLIDE 1: TITLE SLIDE

# 🔥 DEVIN AI MASTERY
## Hidden Features, ACU Optimization & Power Patterns

**From ACU Burner → Power User → Team Multiplier**

Presented by: [Your Name]
Date: June 2026

---

## SLIDE 2: THE PROBLEM WE FACE

### Our Current State
- ✅ Team has basic Devin knowledge
- ❌ ACU consumption is HIGH
- ❌ Same research done by multiple developers
- ❌ No standardized approach
- ❌ GitHub Copilot and Devin used in silos

### The Cost
| Metric | Current | Target |
|--------|---------|--------|
| Avg ACU per bug fix | 4-6 ACUs | 2-3 ACUs |
| Avg ACU per feature | 12-18 ACUs | 6-10 ACUs |
| Monthly ACU burn | ~2,500 | ~1,250 |
| Monthly cost | ~$5,000 | ~$2,500 |
| Duplicate research | 100% | 20% |

### What We'll Cover Today
1. Hidden features most teams don't know exist
2. The ACU optimization framework
3. How to prevent duplicate research across the team
4. Using GitHub Copilot alongside Devin (web-only)
5. Live examples from MY sessions
6. Actionable patterns you can use TODAY

---

## SLIDE 3: MY DEVIN JOURNEY — THE BEFORE & AFTER

### 📅 Month 1: The "Just Ask" Phase
**What I did:**
- Typed vague prompts like "fix the bug"
- No ACU limits set
- Let Devin explore freely
- Accepted whatever Devin produced
- No knowledge sharing with team

**Results:**
- Bug fix: 6 ACUs ($12-14)
- Feature: 18 ACUs ($36-40)
- Build broken 3x/week
- Frustrated with quality
- Teammates repeated my mistakes

### 📅 Month 2: The "Work-Order" Phase
**What I changed:**
- Started using structured prompts
- Set ACU limits per session
- Added acceptance criteria
- Defined scope boundaries

**Results:**
- Bug fix: 4 ACUs ($8-9)
- Feature: 12 ACUs ($24-27)
- Build broken 1x/week
- Quality improved noticeably

### 📅 Month 3: The "Power User" Phase
**What I changed:**
- Built Knowledge base (atomic items)
- Created Playbooks with macros
- Used parallel Devins for multi-file tasks
- Pre-built environment snapshots
- Started sharing knowledge with team
- Used Copilot for exploration, Devin for execution

**Results:**
- Bug fix: 2 ACUs ($4-5)
- Feature: 6 ACUs ($12-14)
- Build never broken by Devin
- PRs ready to merge on first review
- Team stopped duplicating research

---

## SLIDE 4: HIDDEN FEATURE #1 — MANAGED DEVINS (Parallel Execution)

### What It Is
Devin can break down large tasks and delegate to a team of **managed Devins** working in parallel, each in its own isolated VM. The coordinator scopes work, monitors progress, resolves conflicts, and compiles results.

### Most Teams Don't Know This Exists
- They run ONE Devin at a time
- They wait for each task to finish before starting the next
- They never think about parallelization

### Real Example from My Session
**Task:** Migrate 50 files from REST to GraphQL

**BEFORE (Sequential):**
```
"Migrate all files using the old REST client to GraphQL"
→ Devin works on one file at a time
→ 50 files × 2 ACUs = 100 ACUs
→ Took 3 days
```

**AFTER (Parallel with Managed Devins):**
```
"Analyze our codebase for all files using the legacy REST client.
Group them into independent work packages that won't conflict,
then start a parallel Devin session for each package to migrate
to the new GraphQL client. Use the 'REST to GraphQL Migration'
playbook for each session."
```
→ Coordinator Devin analyzes and groups files
→ Spawns 8 child sessions (6-7 files each)
→ Each child runs independently
→ Total: 75 ACUs (25% savings)
→ Finished in 6 hours

### What the Coordinator Can Do
- Spin up managed Devins with specific prompts, playbooks, tags, and ACU limits
- Message child sessions with follow-up instructions
- Monitor ACU consumption per child
- Put child sessions to sleep or terminate them
- Schedule messages to check back on long-running sessions

### When to Use
- Migrations across many files
- Bulk test coverage improvements
- Refactoring across multiple modules
- Any task with 5+ independent work packages

---

## SLIDE 5: HIDDEN FEATURE #2 — WORK-ORDER PROMPTING

### The #1 ACU Killer: Vague Prompts
```
❌ BAD: "Fix the bug in the payment service"
❌ BAD: "Add a new endpoint for user profiles"
❌ BAD: "Refactor the auth code"
```
**Why it burns ACUs:** Devin explores endlessly, refactors files you never asked for, and guesses at requirements.

### The Fix: 6-Section Work-Order Prompt

```markdown
GOAL
  Add a rate limiter to the public signup endpoint. Behavior should match
  the login endpoint's existing rate-limit wrapper. No schema changes.

CONTEXT
  Repo: github.com/acme/acme-web (branch: feature/signup-rate-limit)
  Stack: TypeScript (strict), Next.js 15 App Router, Supabase, Jest.
  Reference implementation: app/api/login/route.ts uses `withRateLimit`
    from lib/rate-limit.ts. Apply the same wrapper to signup.
  Identifier for rate-limiting: IP + email (same as login).

ACCEPTANCE CRITERIA
  1. app/api/signup/route.ts returns HTTP 429 when the rate limit is hit.
  2. Existing signup behavior (201 on success, validation errors on bad
     input) is unchanged.
  3. `npm run typecheck` passes.
  4. `npm run lint` passes.
  5. `npm test` passes, including a new unit test for the signup
     rate-limit path modeled on the login test.
  6. `git diff --name-only` shows only:
       app/api/signup/route.ts
       app/api/signup/route.test.ts
  7. A short summary of the change and commands run.

SCOPE AND NON-GOALS
  In scope:  the signup route and its test file.
  Out of scope: any other route, the rate limiter itself (lib/rate-limit.ts),
    database schema, and dependencies. Do not install new packages.

ENVIRONMENT HINTS
  Install:   `npm ci`
  Test:      `npm test`
  Typecheck: `npm run typecheck`
  Lint:      `npm run lint`
  Env vars needed: SUPABASE_URL, SUPABASE_ANON_KEY (present in the sandbox
    via the configured secrets — do not echo them).

CLOSING STEP
  Open a PR against `staging` titled "feat: rate limit signup endpoint".
  Include the diff summary and command outputs in the PR description.
  Do not merge. Stop after opening the PR.
```

### My Real Results
| Task | Vague Prompt ACU | Work-Order ACU | Savings |
|------|-----------------|----------------|---------|
| Bug fix (auth middleware) | 6 ACUs | 2.5 ACUs | 58% |
| Feature (API endpoint) | 14 ACUs | 6 ACUs | 57% |
| Refactor (error handling) | 10 ACUs | 4 ACUs | 60% |

### Why This Works
- Devin doesn't waste time exploring
- No "helpful" refactors of unrelated files
- Clear stop condition prevents infinite loops
- Pre-defined test commands = fewer iterations

---

## SLIDE 6: HIDDEN FEATURE #3 — ATOMIC KNOWLEDGE BASE

### What 90% of Teams Get Wrong

**❌ WRONG: One giant Knowledge document**
```
"Our Codebase" — 5,000 words covering everything
→ Loaded on EVERY session
→ Burns tokens/ACUs even when irrelevant
```

**✅ RIGHT: 15-20 focused Knowledge items**
```
"Auth Patterns" — 200 words
"DB Migration Rules" — 150 words
"Testing Standards" — 180 words
"PR Template" — 120 words
→ Loaded ONLY when relevant
→ Saves tokens/ACUs on every session
```

### How Knowledge Works
Devin retrieves Knowledge when relevant. A giant document is always loaded (burning tokens/ACUs), while atomic items are loaded only when triggered.

### My Knowledge Setup

| Knowledge Item | Trigger | Content |
|---------------|---------|---------|
| Auth Patterns | `repo:acme-web AND file:*auth*` | JWT handling, refresh tokens, middleware patterns |
| DB Migration Rules | `repo:acme-web AND task:migration` | Always use `npm run migrate:generate` |
| Testing Standards | `repo:acme-web AND task:test` | Jest, mock external APIs, 80% coverage |
| PR Template | `repo:acme-web AND action:pr` | Branch naming: `feat/TICKET-123-short-desc` |
| Error Handling | `repo:acme-web AND file:*error*` | Use `AppError` class, never raw Error |
| Secrets Management | `repo:acme-web AND task:secrets` | Use Devin Secrets dashboard, never paste in prompt |

### Auto-Import from Existing Rules
Devin automatically reads these files from your repo:
- `.rules` files
- `.mdc` files (Cursor rules)
- `.cursorrules` files
- `.windsurf` rules
- `CLAUDE.md` files
- `AGENTS.md` files

**Action Item:** If your team uses Cursor or Claude Code, your rules are ALREADY usable by Devin. Just connect the repo.

### My Pre-Commit Knowledge (Game Changer)
```
Before committing, Devin MUST:
1. Run `npm run lint` — fix all errors
2. Run `npm run typecheck` — fix all errors  
3. Run `npm test` — all tests must pass
4. Run `git diff --name-only` and verify only intended files are changed
5. If any step fails, DO NOT commit. Fix and retry.
```
**Result:** Zero "Devin broke the build" incidents in 30 days. Previously: 2-3 per week.

---

## SLIDE 7: HIDDEN FEATURE #4 — PLAYBOOKS WITH MACROS

### What Is a Playbook?
A reusable template that guides Devin through a specific task type. Think of it as a "recipe" that Devin follows every time.

### My "Add API Endpoint" Playbook

```markdown
# Playbook: Add REST API Endpoint

## Procedure
1. Check existing patterns in `app/api/` for route structure
2. Create new file following the pattern: `app/api/[resource]/route.ts`
3. Implement GET, POST, PUT, DELETE as needed
4. Add Zod validation for all inputs
5. Add error handling using `AppError` class from `src/utils/errors.js`
6. Write tests in `app/api/[resource]/route.test.ts`
7. Run `npm run typecheck && npm run lint && npm test`
8. Open PR with title: `feat: add [resource] endpoint`

## Specifications
- All endpoints must return JSON with consistent envelope: `{ data, error, meta }`
- Use TypeScript strict mode — no `any` types
- Rate limiting applied automatically via middleware

## Advice
- We use CommonJS (require/module.exports), NOT ES modules
- If unsure about DB field names, check `prisma/schema.prisma` first
- Prefer explicit error handling over try/catch
- Use our custom `AppError` class for all errors

## Forbidden Actions
- NEVER modify `prisma/schema.prisma` without explicit approval
- NEVER install new npm packages without checking if existing ones suffice
- NEVER modify files outside `app/api/[resource]/` and its test file
- NEVER merge PRs — always leave them open for human review

## Required from User
- Resource name and expected fields
- Authentication requirements (public, auth, admin)
```

### The Macro Magic
Assign a macro to every playbook:

| Playbook | Macro | Usage |
|----------|-------|-------|
| Add API Endpoint | `!add-endpoint` | `!add-endpoint for /users/profile, auth required` |
| Fix Bug | `!fix-bug` | `!fix-bug in payment service, timeout issue` |
| Write Test | `!write-test` | `!write-test for auth middleware, 80% coverage` |
| Refactor | `!refactor` | `!refactor error handling in payment module` |

**How to use:** Type `!add-endpoint` in the prompt box → full playbook loads instantly. No copy-pasting. No prompt variation.

### Playbook Versioning (New in March 2026)
Playbooks now have version history. When you refine a playbook:
1. Test the new version on 2-3 sessions
2. Compare ACU consumption vs. old version
3. Keep the winner, archive the loser

### My Playbook Stats (from Devin Dashboard)
| Playbook | Sessions | Avg ACU | Merged PRs | Success Rate |
|----------|----------|---------|-----------|--------------|
| !add-endpoint | 24 | 3.2 | 22 | 92% |
| !fix-bug | 18 | 2.1 | 17 | 94% |
| !write-test | 12 | 2.8 | 11 | 92% |
| !refactor | 8 | 4.5 | 7 | 88% |

---

## SLIDE 8: HIDDEN FEATURE #5 — PRE-BUILT SNAPSHOTS

### The Hidden Cost: Setup Tax

Every session, Devin spends 1-2 ACUs on:
- Cloning repos
- Installing dependencies (`npm ci`, `pip install`)
- Configuring environment variables
- Setting up tools

**At 50 sessions/month: 50-100 ACUs wasted on repeat setup!**

### The Fix: Build Once, Use Forever

**Step 1:** Go to Settings > Devin's Machine
**Step 2:** Set up your environment ONCE
**Step 3:** Save as a snapshot
**Step 4:** Every new session starts from this snapshot

### What to Include in Your Snapshot
- All repos cloned and configured
- Dependencies installed (`npm ci`, `pip install`, etc.)
- Environment variables and secrets configured
- Linting and testing tools ready
- Any custom scripts or tools
- Pre-built Docker images if applicable

### My Snapshot Setup
```
Snapshot: "acme-web-dev"
Contents:
  ✓ Repo cloned: github.com/acme/acme-web
  ✓ Branch: develop
  ✓ Dependencies: npm ci completed
  ✓ Secrets: SUPABASE_URL, SUPABASE_ANON_KEY, STRIPE_KEY
  ✓ Tools: ESLint, Prettier, Jest, TypeScript ready
  ✓ Custom scripts: ./scripts/deploy.sh, ./scripts/db-seed.sh
```

### ACU Savings
| Metric | Before Snapshot | After Snapshot |
|--------|----------------|---------------|
| Setup time per session | 15-20 min (1-2 ACUs) | 0 min (0 ACUs) |
| Monthly setup cost | 75-100 ACUs | 0 ACUs |
| Monthly savings | — | $150-200 |

---

## SLIDE 9: HIDDEN FEATURE #6 — CLI HANDOFF PATTERN

### The Split: Local vs. Cloud

**Most teams use EITHER:**
- Cloud Devin for everything (burning ACUs on exploration)
- CLI only (missing async power)

**The Power Pattern: Both, strategically**

### When to Use Devin CLI (FREE — uses your machine)
- Quick exploration and understanding
- Small fixes (< 30 min of work)
- Codebase Q&A
- Interactive coding right in your terminal

### When to Hand Off to Cloud Devin (PAID — uses ACUs)
- Tasks exceeding 30 minutes
- Need VM/server capabilities
- Browser automation (OAuth, screenshots, e2e tests)
- CI/CD pipeline debugging
- Long-running work (migrations, batch jobs)
- Parallel execution

### How to Hand Off
```bash
# In Devin CLI terminal
/handoff fix the flaky integration tests in CI

# Or without task description (continues current work)
/handoff
```

**What carries over:**
- Repo and branch
- Conversation context
- Uncommitted changes (your WIP diff)

### My Real Workflow
```
1. Start Devin CLI locally
2. "Explore the auth module and find where JWT validation happens"
   → FREE, uses my machine
3. "Now fix the bug where expired tokens aren't rejected properly"
   → Still in CLI, quick fix, FREE
4. "Actually, this requires refactoring across 12 files and adding tests"
   → /handoff
   → Cloud Devin takes over with full VM
   → I close my laptop, go to lunch
   → Come back to a PR ready for review
```

### Not Using Devin CLI?
You can hand off from Claude Code, Codex, Cursor, or any coding agent using the open-source Devin Handoff plugin.

---

## SLIDE 10: HIDDEN FEATURE #7 — HARD ACU LIMITS

### The Default Trap
Default ACU limit per session: **10 ACUs**

Most teams never change this. Result: Devin grinds for hours on impossible solutions, burning ACUs.

### My Tiered ACU Limits

| Task Type | ACU Limit | Rationale |
|-----------|-----------|-----------|
| Simple bug fix | 3-5 ACUs | Forces focus, prevents rabbit holes |
| Feature implementation | 8-10 ACUs | Enough for planning + execution + tests |
| Code migration | 15-20 ACUs | Complex, but still bounded |
| Research/exploration | 5 ACUs | Hard stop to prevent endless browsing |

**Where to set:** Settings > Usage > Per-session ACU limit

### What Happens When Limit Is Hit?
Devin stops and asks for direction instead of grinding. You can:
- Extend the limit if the task genuinely needs more
- Redirect Devin to a better approach
- Accept partial results and continue in a new session

### My Experience
**Before limits:**
- Session stuck on dependency conflict for 3 hours
- Burned 12 ACUs ($24-27)
- Had to restart anyway

**After limits:**
- Hit 5 ACU limit on same task
- Devin asked for direction
- I said "skip the dependency update, use existing version"
- Task completed in 3 ACUs total

---

## SLIDE 11: HIDDEN FEATURE #8 — CHECKPOINT PATTERN

### The Problem with One Massive Prompt

```
"Build the entire user profile feature including DB schema,
backend API, frontend form, and tests"
→ Devin plans for 2 hours
→ Implements backend (wrong schema)
→ Implements frontend (based on wrong backend)
→ Tests fail
→ 15 ACUs burned
→ Start over
```

### The Fix: Explicit Checkpoints

```
"First, plan out the database schema changes needed, and let me know 
when that is done so I can apply the migration."
→ WAIT FOR RESPONSE
→ REVIEW AND APPROVE

"Now please implement the backend changes and add tests to make sure 
XYZ works. Let me know when that is done."
→ WAIT FOR RESPONSE
→ REVIEW AND APPROVE

"Now implement the changes in both our web and mobile interfaces to 
call the new backend endpoint."
→ WAIT FOR RESPONSE
→ DONE
```

### My Results
| Approach | Total ACU | Success Rate |
|----------|-----------|-------------|
| One massive prompt | 15 ACUs | 40% |
| Checkpoint pattern | 8 ACUs | 90% |

**Savings: 25-40% because you catch misdirection early**

### Pro Tip: Use Devin's Plan Review
Devin creates a plan before executing. **Always review it.** If the plan is wrong, correct it before Devin starts coding. This is free — no ACUs burned yet.

---

## SLIDE 12: HIDDEN FEATURE #9 — DEVIN REVIEW (Auto Quality Gate)

### What Is Devin Review?
A full-service code review platform within the Devin webapp that turns large, complex PRs into intuitively organized diffs and precise explanations.

### What It Actually Does (Beyond Basic Review)
- **Smart diff organization:** Groups changes logically, not alphabetically
- **Copy/move detection:** Shows changes cleanly instead of full deletes/inserts
- **Bug catcher:** Labels bugs by confidence level
- **Security scanning:** Detects vulnerabilities with CWE classification
- **Codebase-aware chat:** Ask questions about the PR with full context
- **Auto-fix:** Devin can automatically fix flagged issues

### The ACU Size Indicator
| Size | ACU Range | Action |
|------|-----------|--------|
| XS | ≤ 2.25 ACUs | Safe to auto-review |
| S | 2.25 – 4.5 ACUs | Quick manual review |
| M | 4.5 – 9 ACUs | Thorough review recommended |
| L | 9 – 18 ACUs | Deep review + consider breaking into smaller PRs |
| XL | > 18 ACUs | **Break into smaller PRs** — too expensive to review |

### Best Part: Review ACUs Don't Count Against Session Limits
Devin Review draws from a separate enterprise pool. Use it freely.

### How to Access
- Web: app.devin.ai/review
- URL shortcut: Replace `github.com` with `devinreview.com` in any PR URL
- CLI: `npx devin-review {pr-url}`

### My Setup
- Enabled auto-review on all repos
- Auto-fix enabled for Devin-created PRs
- Result: PRs are ready to merge by the time I look at them

---

## SLIDE 13: HIDDEN FEATURE #10 — SCHEDULED SESSIONS

### Set It and Forget It

Set up recurring Devin sessions for maintenance tasks:

| Schedule | Frequency | ACU Cost | Value |
|----------|-----------|----------|-------|
| Dependency audit | Weekly | 2-3 ACUs | Prevents security vulnerabilities |
| Test coverage report | Daily | 1-2 ACUs | Identifies gaps early |
| Documentation sync | Weekly | 2-3 ACUs | Keeps docs current |
| Stale branch cleanup | Weekly | 1 ACU | Reduces repo clutter |
| Sentry error triage | Daily | 2-3 ACUs | Fixes bugs before users report them |

### How to Set Up
```
"Create a schedule that runs every Monday at 8 AM to review
pending knowledge suggestions, deduplicate entries, and resolve
conflicting guidance."
```

### My Scheduled Sessions
```
Monday 8 AM: Dependency audit → Opens PR if updates available
Tuesday 8 AM: Test coverage report → Posts to #dev-team Slack
Wednesday 8 AM: Documentation sync → Updates API docs from code
Friday 5 PM: Stale branch cleanup → Deletes branches older than 30 days
```

**Total weekly ACU cost: ~8 ACUs ($16-18)**
**Value: Prevents emergency fixes that would cost 10-20 ACUs each**

---

## SLIDE 14: HIDDEN FEATURE #11 — DUPLICATE SESSION STRATEGY

### When Uncertain, Run Multiple

When you're not sure about the best approach, start 2-3 duplicate sessions with slightly different prompts.

### My Example: Database Migration Approach

**Session A:**
```
"Migrate the user data from MongoDB to PostgreSQL using a 
streaming approach with batch processing"
```

**Session B:**
```
"Migrate the user data from MongoDB to PostgreSQL using a 
full dump and restore approach"
```

**Session C:**
```
"Migrate the user data from MongoDB to PostgreSQL using an 
event-driven approach with change data capture"
```

### Results
| Session | ACU Used | Approach Quality |
|---------|----------|-----------------|
| A | 3 ACUs | Good for large datasets |
| B | 2 ACUs | Fast but risky for live data |
| C | 4 ACUs | Best for zero-downtime |

**Total: 9 ACUs** to find the best approach
**vs. 1 session grinding for 12 ACUs on a suboptimal approach**

### How to Start Duplicate Sessions
Click "Start duplicate session" button in the sidebar.

---

## SLIDE 15: HIDDEN FEATURE #12 — MCP INTEGRATIONS

### What Is MCP?
Model Context Protocol — connect Devin to external tools and data sources.

### Available Integrations
- **Datadog** — Investigate production issues
- **Sentry** — Triage errors and crashes
- **Databases** — Query data directly
- **Figma** — Read design specs
- **Notion** — Access documentation
- **Stripe** — Check billing/payment data
- **And hundreds more via MCP Marketplace**

### My Setup
```
Connected:
  ✓ Datadog — Devin can check logs and metrics
  ✓ Sentry — Devin can triage errors automatically
  ✓ PostgreSQL — Devin can query production data (read-only)
  ✓ Figma — Devin can read design specs for frontend tasks
```

### Real Example
```
"The payment service is timing out. Check Datadog for error spikes
in the last 24 hours, then fix the root cause in payment_controller.rb"
```
→ Devin checks Datadog → Finds spike at 2 AM → Correlates with deployment → Fixes the issue

**Without MCP:** Devin asks you for logs, you paste them, Devin analyzes → Extra back-and-forth = extra ACUs

---

## SLIDE 16: HIDDEN FEATURE #13 — THE AGENTS TAB & FOCUS MODE

### Agents Tab (For Parallel Sessions)
When a session creates child sessions, an "Agents" tab appears showing:
- Status of each child
- Todos for each child
- PRs opened by each child

**Use this to:** Monitor parallel work without switching between 10 browser tabs.

### Focus Mode
**Shortcut:** Cmd+Shift+F

**What it does:** Hides sidebar, header, and right panel for distraction-free work.

**Why it matters:** Less UI clutter = faster context switching between sessions = more sessions managed per hour.

### Preview Agent Toggle (June 2026)
Enable "Preview upcoming features" in the agent selector for:
- Streaming thoughts (see Devin's reasoning in real-time)
- Faster execution

**Trade-off:** Stability may be limited. Use for well-scoped, low-risk tasks.

---

## SLIDE 17: THE DUPLICATE RESEARCH PROBLEM

### The Scenario You Described

**Developer A (You):**
1. Opened a Devin session
2. Did extensive research (20+ messages)
3. Created implementation plan
4. Created new Devin session for implementation
5. PR merged and closed

**Developer B (Teammate):**
1. Opened a Devin session
2. Did THE SAME extensive research (20+ messages)
3. Created THE SAME implementation plan
4. Did the same work all over again

**WASTE:** Same research × same ACUs × same time = Team-wide inefficiency

### Why This Happens
- No system to capture and share research
- Each developer starts from scratch
- Devin has no memory of past sessions for OTHER developers
- Knowledge exists in individual heads, not in the system

---

## SLIDE 18: THE SOLUTION — RESEARCH TO KNOWLEDGE PIPELINE

### The 6-Step System to Prevent Duplicate Research

### STEP 1: SESSION INSIGHTS — Extract Learnings

**What it is:** After ANY session completes, click the **"Session Insights"** button. Devin analyzes:
- Issue Timeline (color-coded: Red=high impact, Yellow=medium, Green=value)
- Issues Detected (build failures, environment problems, scope ambiguity)
- Actionable Feedback (improved prompt suggestions)
- Session Overview Metrics (ACU usage, messages, size classification)

**How to use:**
```
"Analyze this session where I investigated the payment timeout issue.
Extract the key findings, the root cause, the solution approach,
and any patterns that would help another developer facing the same issue."
```

**Source:** https://docs.devin.ai/product-guides/session-insights

---

## SLIDE 19: STEP 2 — CREATE KNOWLEDGE (Organization-Wide Sharing)

### What It Is
Knowledge is a collection of tips, advice, and instructions that Devin **automatically recalls** across ALL sessions in your organization.

**Key insight:** *"Devin retrieves Knowledge when relevant, not all at once or all at the beginning."*

### How to Create From Your Session
```
"Based on this session's research on the payment timeout issue,
create a Knowledge item that will help any developer who encounters
this issue in the future. Include:
- The symptoms to look for
- The root cause
- The solution approach
- Files that were modified
- Any gotchas or edge cases"
```

### Where It Goes
- **Organization Knowledge** — Visible to ALL members
- **Enterprise Knowledge** — Visible across ALL organizations in your enterprise

### Key Settings
- **Trigger Description:** `repo:acme-web AND (payment OR timeout OR stripe)`
- **Pin to Repo:** Always loaded when working in that repo
- **Macro:** `!payment-timeout-fix` for instant reference

### What Happens Next
When Developer B starts a session mentioning "payment timeout," Devin **AUTOMATICALLY** retrieves this Knowledge. No manual search. No duplicate research.

**Source:** https://docs.devin.ai/product-guides/knowledge

---

## SLIDE 20: STEP 3 — CREATE PLAYBOOK FROM SESSION

### What It Is
Turn a successful session directly into a reusable playbook.

### How to Create
```
"This session successfully diagnosed and fixed a payment timeout issue.
Create a reusable playbook called 'Payment Issue Investigation' that
any on-call engineer can use. Include:
- The investigation procedure
- The debugging commands
- The fix pattern
- The verification steps
- The PR template"
```

### What Devin Produces
- Procedure section
- Specifications
- Advice
- Forbidden actions
- Required from user

### Assign a Macro
`!payment-investigation` — any developer types this and gets your entire research distilled into a template.

**Result:** Developer B doesn't research. They attach the playbook and Devin follows YOUR proven path.

**Source:** https://docs.devin.ai/work-with-devin/advanced-capabilities

---

## SLIDE 21: STEP 4 — SLACK INTEGRATION (Real-Time Sharing)

### What It Is
When you start a session from the web app, click **"Send to channel"** to mirror it in Slack.

### How to Use
1. Start your research session in Devin web
2. Click "Send to channel"
3. Select #dev-team or #incidents
4. Your entire session is mirrored in Slack

### What Teammates See
- Real-time updates on what Devin is doing
- The research path you're taking
- The findings as they emerge
- The final solution

### Result
Developer B sees your session in Slack BEFORE starting their own. They can:
- Follow your research instead of duplicating it
- Add context if they know something you don't
- Wait for your PR instead of starting fresh

**Source:** https://cognition.ai/blog/dec-24-product-update

---

## SLIDE 22: STEP 5 — SCHEDULED KNOWLEDGE MAINTENANCE

### What It Is
Set up recurring Devin sessions to maintain your Knowledge base.

### How to Set Up
```
"Create a schedule that runs every Monday at 8 AM to:
1. Review all knowledge entries for duplicates
2. Merge similar entries
3. Resolve conflicting guidance
4. Identify gaps where multiple developers hit the same issue
   but no knowledge exists"
```

### Where
Settings > Schedules > Create Schedule

### Why This Matters
Without maintenance, your Knowledge base becomes a mess. With maintenance, it becomes a compounding asset.

**Source:** https://docs.devin.ai/product-guides/scheduled-sessions

---

## SLIDE 23: STEP 6 — REPO KNOWLEDGE (Auto-Generated)

### What It Is
Devin automatically scans your repositories and generates understanding of codebase structure, components, and patterns. Shared across ALL sessions.

### How It Helps
- When Developer B starts a session, Devin ALREADY knows your codebase
- No need to re-explain architecture, file structure, or conventions
- The "exploration" phase is dramatically shortened

### Where to Find
Settings & Library > Knowledge > Repo Knowledge

**Source:** https://cognition.ai/blog/dec-24-product-update

---

## SLIDE 24: THE COMPLETE PIPELINE VISUALIZED

```
DEVELOPER A's RESEARCH SESSION (8 ACUs, 20 messages)
        ↓
SESSION INSIGHTS (Click button → free analysis)
        ↓
    ┌───┴───┐
    ↓       ↓
KNOWLEDGE   PLAYBOOK
(Auto-retrieved)  (!macro-name)
    ↓       ↓
    └───┬───┘
        ↓
SLACK SHARE (Real-time visibility)
        ↓
DEVELOPER B starts session
        ↓
Devin AUTO-RETRIEVES Knowledge
        ↓
Devin SUGGESTS Playbook
        ↓
Developer B attaches playbook
        ↓
Devin follows YOUR proven path
        ↓
2 ACUs used (vs 8 for you) → 75% savings
```

### The Golden Rule
> **"Every research session MUST produce Knowledge or a Playbook. No exceptions."**

**Enforcement:**
- Add to your team's Definition of Done for Devin sessions
- Sprint retrospective question: "What Knowledge did we create this sprint?"
- Track: Knowledge items per developer per week

---

## SLIDE 25: USING GITHUB COPILOT ALONGSIDE DEVIN

### The Reality Check

**You have:**
- ✅ Devin web access only
- ✅ GitHub Copilot in your IDE
- ❌ No Devin CLI (no `/handoff`)
- ❌ No Devin IDE extension

**The Truth:** There is **NO direct integration** between Copilot and Devin. They are separate products from separate companies.

**The Opportunity:** You can still build a powerful hybrid workflow.

---

## SLIDE 26: THE HYBRID WORKFLOW — COPILOT FOR SPEED, DEVIN FOR DEPTH

### Phase 1: Local Exploration with Copilot (FREE)

**What Copilot Excels At:**
- Inline code suggestions as you type
- Quick function implementations
- Small refactors (rename, extract method)
- Explaining code blocks
- Generating unit tests for single functions
- Chat-based Q&A about your codebase

**What to Do:**
```
1. Open your IDE with Copilot enabled
2. Use Copilot Chat to explore:
   "Why is the payment service timing out?"
   "Show me where JWT validation happens"
   "Explain this error handling pattern"

3. Use Copilot inline to:
   - Draft quick fixes
   - Generate test stubs
   - Refactor small functions

4. Use Copilot's @workspace to:
   - Search across your codebase
   - Find related files
```

**Cost:** $0 (your Copilot subscription)
**Time:** 10-15 minutes

---

## SLIDE 27: THE HYBRID WORKFLOW — DECISION POINT

### Use Copilot When:
- The fix is in 1-3 files
- You know exactly what needs to change
- It's a pattern you've done before
- You want to stay in flow state
- Time estimate: < 30 minutes

### Use Devin When:
- The task spans 3+ files
- You need research and investigation
- You need tests, lint, and PR creation
- You want to delegate and walk away
- Time estimate: > 30 minutes
- You need browser automation (OAuth, screenshots)

---

## SLIDE 28: THE STRUCTURED PROMPT TRANSFER TECHNIQUE

### Since You Don't Have CLI Handoff

**Step 1 — In Copilot Chat:**
```
"Summarize the issue, root cause, and proposed fix for the payment
timeout bug. Format it as a structured implementation plan."
```

**Step 2 — Copilot Generates:**
```markdown
## Issue Summary
Payment service times out after 30s on Stripe webhook processing

## Root Cause
Webhook handler doesn't use async processing

## Proposed Fix
1. Make webhook handler async
2. Add background job queue
3. Update tests

## Files to Modify
- app/api/webhooks/stripe.ts
- lib/jobs/payment-jobs.ts (new)
- app/api/webhooks/stripe.test.ts

## Acceptance Criteria
- Webhook responds in < 2s
- Events processed asynchronously
- All tests pass
```

**Step 3 — Copy into Devin Web:**
```
GOAL
  Fix payment service timeout by making Stripe webhook handler async

CONTEXT
  [Paste Copilot's analysis here]
  Repo: github.com/acme/acme-web
  Stack: TypeScript, Next.js, Prisma, Jest

ACCEPTANCE CRITERIA
  [Paste from Copilot's plan]

SCOPE
  In scope: [list files from Copilot]
  Out of scope: Any other webhook handlers, database schema changes

ENVIRONMENT
  Install: npm ci
  Test: npm test
  Lint: npm run lint

CLOSING STEP
  Open PR titled "fix: async stripe webhook processing"
  Do not merge
```

---

## SLIDE 29: THE ACU MATH — COPILOT + DEVIN vs DEVIN ALONE

### Scenario: Implement a New API Endpoint

**Devin Alone:**
```
"Add a user profile endpoint"
→ Devin researches codebase: 2 ACUs
→ Devin plans implementation: 1 ACU
→ Devin implements: 3 ACUs
→ Devin writes tests: 2 ACUs
→ Devin opens PR: 0.5 ACU
Total: 8.5 ACUs ($17-19)
```

**Copilot + Devin:**
```
Copilot: "Generate a user profile endpoint following our patterns"
→ Copilot suggests code inline: 0 ACUs

You: Refine in IDE with Copilot: 0 ACUs

Devin: "I've drafted the endpoint. Please add tests, run lint, open PR"
→ Devin tests + lint + PR: 2 ACUs
Total: 2 ACUs ($4-5)
```

**Savings: 6.5 ACUs = $13-14 per task**

---

## SLIDE 30: THE BRANCH HANDOFF TECHNIQUE

### For Complex Tasks: Copilot Drafts, Devin Finishes

**Step 1 — In your IDE with Copilot:**
```bash
git checkout -b wip/payment-fix-copilot-draft
# Write code with Copilot suggestions
git add .
git commit -m "wip: draft payment fix with copilot"
git push origin wip/payment-fix-copilot-draft
```

**Step 2 — In Devin Web:**
```
GOAL
  Complete the payment fix implementation. I've drafted the initial
  code in branch wip/payment-fix-copilot-draft. Please:
  1. Review the draft implementation
  2. Add missing error handling
  3. Write comprehensive tests
  4. Run lint and typecheck
  5. Open a PR against develop

CONTEXT
  Branch: wip/payment-fix-copilot-draft
  Base branch: develop
  Stack: [your stack]
```

**Result:**
- Copilot did creative work (free)
- Devin did mechanical work (minimal ACUs)
- GitHub is the bridge between them

---

## SLIDE 31: THE KNOWLEDGE BRIDGE FOR YOUR TEAM

### Document the Hybrid Pattern in Devin Knowledge

```markdown
Title: "Copilot → Devin Handoff Pattern"
Trigger: repo:acme-web AND task:implementation

Content:
When starting a new implementation task:
1. FIRST use Copilot in IDE to:
   - Explore the codebase (free)
   - Draft initial code (free)
   - Understand existing patterns (free)

2. THEN use Devin Web for:
   - Multi-file changes (paid)
   - Test writing (paid)
   - Lint/typecheck enforcement (paid)
   - PR creation (paid)

3. When handing off to Devin, ALWAYS include:
   - Copilot's analysis/summary
   - Draft code you've written
   - Design decisions made with Copilot
   - Any gotchas Copilot identified
```

**Result:** Your entire team follows the same hybrid pattern, maximizing Copilot (free) and minimizing Devin ACUs.

---

## SLIDE 32: LIMITATIONS & WORKAROUNDS

| Limitation | Workaround |
|-----------|-----------|
| No CLI handoff | Use "Structured Prompt Transfer" (copy Copilot analysis into Devin prompt) |
| No IDE extension | Use browser + IDE side-by-side, or Devin web on second monitor |
| No local file sync | Commit Copilot drafts to a branch, tell Devin to work from that branch |
| No real-time sync | Use GitHub as the bridge — commit Copilot work, Devin picks it up |
| No direct integration | Build Knowledge items that document the hybrid workflow |

---

## SLIDE 33: MY PERSONAL IMPROVEMENT METRICS

### The Numbers Don't Lie

| Metric | Month 1 | Month 2 | Month 3 | Improvement |
|--------|---------|---------|---------|-------------|
| Avg ACU per session | 8.5 | 5.2 | 3.1 | 64% ↓ |
| Sessions per week | 5 | 8 | 12 | 140% ↑ |
| PRs merged per week | 3 | 6 | 10 | 233% ↑ |
| Build breaks by Devin | 3/week | 1/week | 0/week | 100% ↓ |
| Time to first PR review | 2 days | 1 day | 4 hours | 75% ↓ |
| Monthly ACU cost | $850 | $520 | $310 | 64% ↓ |
| Duplicate research | 100% | 60% | 20% | 80% ↓ |
| Copilot + Devin hybrid tasks | 0% | 30% | 70% | — |

### What Changed Each Month

**Month 1 → Month 2:**
- Started using Work-Order Prompting
- Set ACU limits per session
- Added acceptance criteria to every prompt

**Month 2 → Month 3:**
- Built atomic Knowledge base (15 items)
- Created 4 Playbooks with macros
- Started using parallel Devins
- Built pre-configured snapshot
- Enabled Devin Review with auto-fix
- Started using Copilot for exploration, Devin for execution
- Created Knowledge sharing pipeline with team

### The Compound Effect
Each optimization builds on the previous one. It's not just one thing — it's the SYSTEM.

---

## SLIDE 34: THE 30-DAY TRANSFORMATION PLAN

### Week 1: Foundation
- [ ] Audit current ACU consumption (check dashboard)
- [ ] Create 3-5 atomic Knowledge items for your top repos
- [ ] Set up repo snapshots with all dependencies pre-installed
- [ ] Set default ACU limits: 5 for bugs, 10 for features

### Week 2: Playbooks & Knowledge Sharing
- [ ] Identify your 3 most common task types
- [ ] Create playbooks for each with macros
- [ ] Test playbooks and measure ACU consumption
- [ ] After every research session, create Knowledge or Playbook
- [ ] Share sessions to Slack #dev-team

### Week 3: Parallelization & Hybrid Workflow
- [ ] Identify a multi-file task suitable for parallel Devins
- [ ] Use "Devin manages Devins" to delegate
- [ ] Measure total ACU vs. sequential approach
- [ ] Try Copilot exploration → Devin execution on 3 tasks
- [ ] Document the hybrid pattern in Knowledge

### Week 4: Automation & Maintenance
- [ ] Set up 2-3 scheduled sessions for maintenance
- [ ] Configure Slack-to-Devin pipeline for bug reports
- [ ] Enable Devin Review on your most active repos
- [ ] Set up weekly Knowledge maintenance schedule
- [ ] Review monthly ACU consumption — target 40-50% reduction
- [ ] Track duplicate research reduction — target 80%

---

## SLIDE 35: THE 10 ANTI-PATTERNS TO AVOID

| # | Anti-Pattern | Why It Burns ACUs | The Fix |
|---|-------------|-------------------|---------|
| 1 | "Fix the bug" (vague) | Devin explores endlessly | Use Work-Order Prompting |
| 2 | No ACU limits | Runaway sessions | Set 5-10 ACU default limit |
| 3 | One giant Knowledge doc | Loaded every session | Atomic Knowledge items |
| 4 | No repo snapshot | 2 ACUs wasted on setup each time | Pre-build environment |
| 5 | Letting stuck sessions grind | 5+ ACUs on impossible solutions | Stop, redirect, or restart |
| 6 | Skipping plan review | Wrong direction for hours | Always review the plan first |
| 7 | No out-of-scope list | "Helpful" refactors burn ACUs | Explicitly list forbidden files |
| 8 | Secrets in prompts | Security risk + wasted tokens | Use Secrets dashboard |
| 9 | No acceptance criteria | Devin guesses "done" | Define verifiable success |
| 10 | Ignoring Session Insights | Repeat same mistakes | Review after every session |
| 11 | Not sharing research | Teammates duplicate work | Create Knowledge after every session |
| 12 | Using Devin for everything | Wasting ACUs on small tasks | Use Copilot for exploration, Devin for execution |
| 13 | No Knowledge maintenance | Knowledge base becomes stale | Weekly scheduled maintenance |

---

## SLIDE 36: QUICK REFERENCE CARD

### Essential Shortcuts
| Shortcut | Action |
|----------|--------|
| Cmd+K / Ctrl+K | Command palette — start session, switch org |
| Cmd+Shift+F | Focus mode |
| `!macro-name` | Attach playbook instantly |
| `/handoff` | Send CLI session to cloud |

### Essential Settings
| Setting | Location | Recommendation |
|---------|----------|---------------|
| ACU limit per session | Settings > Usage | 5-10 default |
| Auto-approve plans | Settings > Customization | OFF for complex tasks |
| Slack notifications | Settings > Profile | ON |
| Default filters | Session list > Filter icon | Save as default |

### Essential Files to Create
| File | Purpose |
|------|---------|
| `AGENTS.md` (repo root) | Project rules for Devin CLI |
| `.devin/config.yaml` | Custom tools and commands |
| `.github/PULL_REQUEST_TEMPLATE/devin_pr_template.md` | PR template for Devin |
| `SECURITY.md` | Custom security policies for Devin Review |

---

## SLIDE 37: REFERENCES & RESOURCES

### Official Devin Documentation
1. **Devin Docs — Introducing Devin**
   https://docs.devin.ai/get-started/devin-intro

2. **Devin Docs — When to Use Devin (Best Practices)**
   https://docs.devin.ai/essential-guidelines/when-to-use-devin

3. **Devin Docs — Advanced Capabilities (Managed Devins)**
   https://docs.devin.ai/work-with-devin/advanced-capabilities

4. **Devin Docs — Using Playbooks**
   https://docs.devin.ai/product-guides/using-playbooks

5. **Devin Docs — Devin CLI**
   https://docs.devin.ai/work-with-devin/devin-cli

6. **Devin Docs — Hand Off to Cloud Devins**
   https://docs.devin.ai/work-with-devin/devin-handoff

7. **Devin Docs — Devin Review**
   https://docs.devin.ai/work-with-devin/devin-review

8. **Devin Docs — Best Practices & Use Cases**
   https://docs.devin.ai/use-cases/best-practices

9. **Devin Docs — Release Notes Overview**
   https://docs.devin.ai/release-notes/overview

10. **Devin Docs — Devin MCP**
    https://docs.devin.ai/work-with-devin/devin-mcp

11. **Devin Docs — Session Insights**
    https://docs.devin.ai/product-guides/session-insights

12. **Devin Docs — Knowledge**
    https://docs.devin.ai/product-guides/knowledge

13. **Devin Docs — Scheduled Sessions**
    https://docs.devin.ai/product-guides/scheduled-sessions

### Community & Blogs
14. **Cognition Blog — Devin Case Studies**
    https://www.cognition.dev/blog

15. **Devin Community Gallery (Playbooks)**
    https://app.devin.ai/settings/playbooks

### Tools
16. **Devin Handoff GitHub Plugin (Open Source)**
    https://github.com/cognition-labs/devin-handoff

17. **Devin MCP Marketplace**
    https://mcp.devin.ai/

### GitHub Copilot
18. **Copilot Chat Documentation**
    https://docs.github.com/en/copilot/using-github-copilot/copilot-chat

19. **Getting Started with Copilot**
    https://docs.github.com/en/copilot/using-github-copilot/getting-started-with-github-copilot

---

## SLIDE 38: Q&A

### Questions?

**My direct messages are open for:**
- Help setting up your first playbook
- Reviewing your work-order prompts
- Debugging high ACU consumption
- Sharing successful patterns
- Setting up the Knowledge sharing pipeline
- Configuring the Copilot + Devin hybrid workflow

### Remember
> "Devin replaces TASKS, not ROLES. The teams that win invest in setup 
> (Knowledge, snapshots, playbooks) BEFORE burning ACUs."

**Expected Result for our team:**
- 40-60% ACU reduction in 30 days
- 80% reduction in duplicate research
- 2-3x team velocity improvement

---

*Presentation compiled from official Devin documentation, release notes, and real-world enterprise case studies. Last updated: June 2026.*
