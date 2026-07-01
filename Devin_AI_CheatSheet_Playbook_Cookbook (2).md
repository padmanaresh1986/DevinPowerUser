
# 🔥 DEVIN AI: THE ULTIMATE CHEAT SHEET, PLAYBOOK & COOKBOOK
## Hidden Features, ACU Optimization & Power-User Patterns
### Version: June 2026 | Compiled for Enterprise Teams

---

## 📊 EXECUTIVE SUMMARY

Your team is burning ACUs because they're using Devin like a chatbot instead of an autonomous agent. This guide transforms your developers from casual users into Devin architects who get 3-5x more output per ACU.

**Key Stats:**
- 1 ACU = ~15 minutes of active Devin work ($2.00-$2.25)
- Well-scoped tasks: 1-3 ACUs | Poorly scoped tasks: 5-15+ ACUs
- Parallel sessions can reduce total project ACU burn by 40-60%
- Playbooks reduce per-task ACU consumption by 30-50% after the 3rd iteration

---

## 🎯 PART 1: THE ACU OPTIMIZATION FRAMEWORK

### 1.1 The #1 ACU Killer: Scope Creep

**The Problem:** Devin is "helpful" — it will refactor adjacent files, upgrade dependencies, and "improve" code you never asked it to touch. Every extra file = extra ACUs.

**The Fix — Work-Order Prompting:**

```
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

**Why This Saves ACUs:**
- Devin doesn't waste time exploring the codebase
- No "helpful" refactors of unrelated files
- Clear stop condition prevents infinite loops
- Pre-defined test commands = fewer iterations

### 1.2 Set Hard ACU Limits Per Session

**Hidden Setting:** You can configure per-session ACU limits in Settings > Usage. Default is 10 ACUs.

**Best Practice Tiers:**
| Task Type | Recommended ACU Limit | Rationale |
|-----------|----------------------|-----------|
| Simple bug fix | 3-5 ACUs | Forces focus, prevents rabbit holes |
| Feature implementation | 8-10 ACUs | Enough for planning + execution + tests |
| Code migration | 15-20 ACUs | Complex, but still bounded |
| Research/exploration | 5 ACUs | Hard stop to prevent endless browsing |

**Pro Tip:** Set limits BEFORE starting the session. You can always extend if needed, but you can't recover burned ACUs.

### 1.3 The "Checkpoint Pattern" — Stop & Verify

Instead of one massive prompt, break into checkpoints:

```
"First, plan out the database schema changes needed, and let me know 
when that is done so I can apply the migration."
→ WAIT FOR RESPONSE

"Now please implement the backend changes and add tests to make sure 
XYZ works. Let me know when that is done."
→ WAIT FOR RESPONSE

"Now implement the changes in both our web and mobile interfaces to 
call the new backend endpoint."
```

**ACU Savings:** 25-40% because you catch misdirection early instead of letting Devin grind for hours on the wrong path.

### 1.4 Use `/handoff` for the CLI → Cloud Split

**The Pattern:**
1. **Local (Devin CLI):** Quick exploration, small fixes, understanding codebase — uses YOUR compute, not ACUs
2. **Cloud Handoff:** When the task exceeds 30 min of work, type `/handoff` to send to cloud Devin

**Why This Works:**
- Local CLI is free (uses your machine)
- You validate the approach locally before burning cloud ACUs
- Cloud Devin picks up exactly where CLI left off

---

## 🧠 PART 2: KNOWLEDGE BASE — THE HIDDEN MULTIPLIER

### 2.1 What 90% of Teams Get Wrong

Most teams create ONE giant Knowledge document. **This is wrong.**

**The Correct Pattern — Atomic Knowledge:**

```
❌ BAD: One 5,000-word "Our Codebase" document
✅ GOOD: 15-20 focused Knowledge items, each <500 words
```

**Why:** Devin retrieves Knowledge when relevant. A giant document is always loaded (burning tokens/ACUs), while atomic items are loaded only when triggered.

### 2.2 Knowledge Trigger Strategy

Create Knowledge items with **highly specific triggers**:

| Knowledge Item | Trigger | Content |
|---------------|---------|---------|
| "Auth Patterns" | `repo:acme-web AND file:*auth*` | How we handle JWT, refresh tokens, middleware |
| "DB Migration Rules" | `repo:acme-web AND task:migration` | Always use `npm run migrate:generate`, never edit schema directly |
| "Testing Standards" | `repo:acme-web AND task:test` | Use Jest, mock external APIs, 80% coverage minimum |
| "PR Template" | `repo:acme-web AND action:pr` | Branch naming: `feat/TICKET-123-short-desc` |

### 2.3 Auto-Import from Existing Rules

Devin automatically reads these files from your repo:
- `.rules` files
- `.mdc` files (Cursor rules)
- `.cursorrules` files
- `.windsurf` rules
- `CLAUDE.md` files
- `AGENTS.md` files

**Action Item:** If your team uses Cursor or Claude Code, your rules are ALREADY usable by Devin. Just connect the repo.

### 2.4 The "Pre-Commit Knowledge" Hack

Add this to your Knowledge to prevent bad commits:

```
Before committing, Devin MUST:
1. Run `npm run lint` — fix all errors
2. Run `npm run typecheck` — fix all errors  
3. Run `npm test` — all tests must pass
4. Run `git diff --name-only` and verify only intended files are changed
5. If any step fails, DO NOT commit. Fix and retry.
```

**Result:** No more "Devin broke the build" — saves 2-5 ACUs per failed CI cycle.

---

## 📋 PART 3: PLAYBOOKS — YOUR ACU-SAVING TEMPLATES

### 3.1 The Anatomy of a Killer Playbook

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

### 3.2 Playbook Macros — The Speed Hack

Assign a macro to every playbook: `!add-endpoint`, `!fix-bug`, `!write-test`

**Usage:**
```
!add-endpoint for the /users/profile route. Auth required.
```

**Result:** Full playbook loads instantly. No more copy-pasting prompts.

### 3.3 Playbook Versioning

Playbooks now have version history (March 2026 update). When you refine a playbook:
1. Test the new version on 2-3 sessions
2. Compare ACU consumption vs. old version
3. Keep the winner, archive the loser

**Pro Tip:** The Playbook page shows session count, unique users, and merged PRs per playbook. Use this data to identify your highest-ROI playbooks.

---

## 🤖 PART 4: MANAGED DEVINS — PARALLEL EXECUTION

### 4.1 The "Devin Manages Devins" Pattern (March 2026)

This is the single most powerful feature most teams don't use.

**How It Works:**
1. Start ONE coordinator session
2. Ask Devin to break the task into independent work packages
3. Devin spins up child sessions (each with its own VM and ACU limit)
4. Coordinator monitors progress, resolves conflicts, compiles results

**Example — 50-File Migration:**
```
"Analyze our codebase for all files using the legacy REST client.
Group them into independent work packages that won't conflict,
then start a parallel Devin session for each package to migrate
to the new GraphQL client. Use the 'REST to GraphQL Migration'
playbook for each session."
```

**ACU Math:**
- Sequential: 50 files × 2 ACUs = 100 ACUs
- Parallel: 50 files × 1.5 ACUs (faster per task) = 75 ACUs
- **Savings: 25%** + results in hours instead of days

### 4.2 The Batch Test Coverage Pattern

```
"Run the test coverage report, find the 8 modules below 50%
coverage, and start a parallel Devin session for each module
using our test-writing playbook. Open a separate PR for each."
```

**Result:** 8 PRs created simultaneously. Review and merge at your pace.

### 4.3 Child Session ACU Management

Each child session can have its OWN ACU limit:
```
"Start 5 parallel sessions, each with a 3 ACU limit, to update
all repositories in our org to the new logging library."
```

**Safety Net:** If one child gets stuck, it burns only 3 ACUs, not the whole budget.

---

## 🔧 PART 5: ENVIRONMENT & SETUP OPTIMIZATION

### 5.1 The Blueprint/Snapshot System

**Critical Insight:** Devin's workspace resets at the start of EVERY session. If Devin spends 2 ACUs setting up the environment each time, you're burning 40% of your budget on repeat work.

**The Fix — Pre-Built Snapshots:**

1. Go to Settings > Devin's Machine
2. Set up your environment ONCE with all dependencies, secrets, and tools
3. Save as a snapshot
4. Every new session starts from this snapshot — zero setup time

**What to Include in Your Snapshot:**
- All repos cloned and configured
- Dependencies installed (`npm ci`, `pip install`, etc.)
- Environment variables and secrets configured
- Linting and testing tools ready
- Any custom scripts or tools

**ACU Savings:** 1-2 ACUs per session × 50 sessions/month = 50-100 ACUs saved

### 5.2 The `.devin/config.yaml` File

Create this file in your repo root to define custom tools:

```yaml
tools:
  - name: deploy_to_staging
    command: ./scripts/deploy.sh staging
    description: "Use this to deploy code to the staging environment after tests pass."

  - name: run_e2e_tests
    command: npm run test:e2e
    description: "Run end-to-end tests. Only use after unit tests pass."

  - name: check_db_migrations
    command: npx prisma migrate status
    description: "Check pending database migrations before deploying."
```

**Why This Saves ACUs:** Devin doesn't waste time figuring out how to run tests or deploy. It uses your pre-defined commands.

### 5.3 Secrets Management — The Right Way

**NEVER paste secrets in prompts.** This is both a security risk AND an ACU waste (Devin might echo them in logs).

**Correct Approach:**
1. Add secrets in Devin Dashboard > Secrets
2. Reference them by name in prompts: "Use the SUPABASE_URL secret"
3. For bulk secrets, use `.env` files with `direnv`

**New Feature (March 2026):** You can now attach secrets directly when creating a session from the home page.

---

## 🔄 PART 6: AUTOMATION & SCHEDULED SESSIONS

### 6.1 Recurring Maintenance Sessions

Set up automated sessions that run on schedule:

```
"Create a schedule that runs every Monday at 8 AM to review
pending knowledge suggestions, deduplicate entries, and resolve
conflicting guidance."
```

**Other High-Value Schedules:**
| Schedule | Frequency | ACU Cost | Value |
|----------|-----------|----------|-------|
| Dependency audit | Weekly | 2-3 ACUs | Prevents security vulnerabilities |
| Test coverage report | Daily | 1-2 ACUs | Identifies gaps early |
| Documentation sync | Weekly | 2-3 ACUs | Keeps docs current |
| Stale branch cleanup | Weekly | 1 ACU | Reduces repo clutter |

### 6.2 Slack-to-Code Pipeline

**Setup:**
1. Connect Devin to your Slack workspace
2. In #bugs channel: "@Devin The payment service is timing out. Check `payment_controller.rb`"
3. Devin creates a session, fixes the bug, opens a PR
4. PR link posted back to Slack

**ACU Optimization:** The Slack integration includes thread context, so Devin doesn't waste ACUs asking for background.

### 6.3 Jira/Linear Integration

**Hidden Feature:** You can assign tickets DIRECTLY to Devin in Jira/Linear. Devin reads the ticket description, acceptance criteria, and comments — then starts working.

**ACU Tip:** Add a "Devin Context" field to your tickets with file paths and relevant docs. This saves 0.5-1 ACU per ticket.

---

## 🛡️ PART 7: DEVIN REVIEW — THE QUALITY GATE

### 7.1 What Devin Review Actually Does

Devin Review doesn't just comment on PRs. It:
- Groups related changes logically
- Detects copied/duplicated code
- Identifies bugs and security issues
- Respects your `SECURITY.md` file for custom security policies
- Provides inline chat for questions

### 7.2 ACU-Aware Review Strategy

**Review Size Indicator (New Feature):**
| Size | ACU Range | Action |
|------|-----------|--------|
| XS | ≤ 2.25 ACUs | Safe to auto-review |
| S | 2.25 – 4.5 ACUs | Quick manual review |
| M | 4.5 – 9 ACUs | Thorough review recommended |
| L | 9 – 18 ACUs | Deep review + consider breaking into smaller PRs |
| XL | > 18 ACUs | **Break into smaller PRs** — too expensive to review |

**Pro Tip:** Devin Review ACUs do NOT count against your org's session ACU limits. They draw from a separate enterprise pool.

### 7.3 The "Repo Rule" Badge

When Devin Review flags an issue from your `.rules` or `AGENTS.md` files, it shows a "Repo rule" badge. This helps distinguish your custom rules from general analysis.

---

## 📈 PART 8: ANALYTICS & CONTINUOUS IMPROVEMENT

### 8.1 Session Insights — Your ACU Audit Tool

**New Feature (March 2026):** On-demand session insights.

**How to Use:**
1. Click "View Session Insights" on any session
2. Review the timeline of events
3. Identify where Devin spent the most time
4. Check "Actionable Feedback" for prompt improvement suggestions

**What to Look For:**
- Long browser sessions = Devin was confused by docs (add Knowledge)
- Multiple test failures = unclear acceptance criteria (refine prompt)
- File exploration loops = missing breadcrumbs (add file paths to prompt)

### 8.2 The Consumption Dashboard

**Enterprise Features:**
- Top 10 repositories by ACU consumption
- Top 10 users by ACU consumption  
- Per-repo review ACU breakdown
- Daily consumption charts

**Actionable Insight:** If one repo consumes 40% of ACUs, that's your playbook candidate.

### 8.3 The Feedback Loop

After EVERY session, ask:
1. "What Knowledge should I add to prevent this issue next time?"
2. "Can this successful session become a Playbook?"
3. "Where did Devin waste time?"

**Compound Effect:** After 4 weeks of this practice, your team's ACU efficiency improves 40-60%.

---

## 🚀 PART 9: ADVANCED PATTERNS & HACKS

### 9.1 The "Role Play" Prompt

```
"Act as a Senior SRE. Focus on reliability, observability, and 
logging. Add structured logging to all new functions. Include 
metrics and tracing."
```

**Result:** Devin produces production-grade code with monitoring built-in, reducing post-deployment fixes.

### 9.2 The "Pseudocode First" Pattern

For complex logic, provide pseudocode:

```
"Implement a rate limiter middleware for Express using Redis. 
Follow this logic:

// pseudocode
if key exists in redis:
  increment count
  if count > limit: return 429
else:
  set key with expiry

Use our existing Redis client from lib/redis.ts."
```

**ACU Savings:** 20-30% because Devin doesn't explore wrong implementations.

### 9.3 The "Duplicate Session" Strategy

**Hidden Feature:** "Start duplicate session" button in the sidebar.

**When to Use:**
- Uncertain about the best approach? Start 2-3 sessions with slightly different prompts.
- Compare results and merge the best parts.
- **ACU Math:** 3 sessions × 2 ACUs = 6 ACUs vs. 1 session that grinds for 8 ACUs on a suboptimal path.

### 9.4 The "Preview Agent" Toggle

**New Feature (June 2026):** Enable "Preview upcoming features" in the agent selector.

**What It Does:**
- Streaming thoughts (see Devin's reasoning in real-time)
- Faster execution
- **Trade-off:** Stability may be limited

**When to Use:** For well-scoped, low-risk tasks where speed matters more than reliability.

### 9.5 The "Focus Mode" Hack

**Shortcut:** Cmd+Shift+F

**What It Does:** Hides sidebar, header, and right panel for distraction-free work.

**Why It Matters:** Less UI clutter = faster context switching between sessions = more sessions managed per hour.

### 9.6 The "Agents Tab" for Child Sessions

When a session creates child sessions, an "Agents" tab appears showing:
- Status of each child
- Todos for each child
- PRs opened by each child

**Use This To:** Monitor parallel work without switching between 10 browser tabs.

---

## 🎓 PART 10: THE 30-DAY TRANSFORMATION PLAN

### Week 1: Foundation
- [ ] Audit current ACU consumption (check dashboard)
- [ ] Create 3-5 atomic Knowledge items for your top repos
- [ ] Set up repo snapshots with all dependencies pre-installed
- [ ] Set default ACU limits: 5 for bugs, 10 for features

### Week 2: Playbooks
- [ ] Identify your 3 most common task types
- [ ] Create playbooks for each with macros
- [ ] Test playbooks and measure ACU consumption
- [ ] Refine based on results

### Week 3: Parallelization
- [ ] Identify a multi-file task suitable for parallel Devins
- [ ] Use "Devin manages Devins" to delegate
- [ ] Measure total ACU vs. sequential approach
- [ ] Document the winning pattern

### Week 4: Automation
- [ ] Set up 2-3 scheduled sessions for maintenance
- [ ] Configure Slack-to-Devin pipeline for bug reports
- [ ] Enable Devin Review on your most active repos
- [ ] Review monthly ACU consumption — target 40-50% reduction

---

## ⚠️ PART 11: COMMON ANTI-PATTERNS TO AVOID

| Anti-Pattern | Why It Burns ACUs | The Fix |
|-------------|-------------------|---------|
| "Fix the bug" (vague) | Devin explores endlessly | Use Work-Order Prompting |
| No ACU limits | Runaway sessions | Set 5-10 ACU default limit |
| One giant Knowledge doc | Loaded every session | Atomic Knowledge items |
| No repo snapshot | 2 ACUs wasted on setup each time | Pre-build environment |
| Letting stuck sessions grind | 5+ ACUs on impossible solutions | Stop, redirect, or restart |
| Skipping plan review | Wrong direction for hours | Always review the plan first |
| No out-of-scope list | "Helpful" refactors burn ACUs | Explicitly list forbidden files |
| Secrets in prompts | Security risk + wasted tokens | Use Secrets dashboard |
| No acceptance criteria | Devin guesses "done" | Define verifiable success |
| Ignoring Session Insights | Repeat same mistakes | Review after every session |

---

## 💡 BONUS: THE "GOLDMAN SACHS" WORKFLOW

Goldman Sachs' reported approach (12,000 developers, 80 PRs/week):
1. **Dedicated Devin Orchestrator Role:** One person manages Devin delegation
2. **Structured Task Types Only:** Bug fixes, tests, docs, migrations — NOT architecture
3. **50%+ Acceptance Rate:** They review and iterate on prompts, not just accept output
4. **Knowledge Base Investment:** Heavy upfront investment in codebase context
5. **Hybrid Workforce:** Senior engineers architect, Devin executes the backlog

**Key Takeaway:** Enterprise results require enterprise-level investment in setup, not just throwing ACUs at problems.

---

## 📚 QUICK REFERENCE CARD

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

## 🏁 CONCLUSION

Devin is not a magic button — it's a force multiplier that requires strategic investment. The teams that win are the ones that:

1. **Invest in setup** (Knowledge, snapshots, playbooks) BEFORE burning ACUs
2. **Treat prompts as engineering artifacts** — versioned, tested, refined
3. **Use parallelization** for multi-file tasks
4. **Monitor and iterate** using Session Insights and consumption analytics
5. **Set boundaries** — ACU limits, scope definitions, forbidden actions

**Your team's ACU consumption should drop 40-60% within 30 days of implementing these patterns.**

---

*Compiled from official Devin documentation, community best practices, and real-world enterprise case studies. Last updated: June 2026.*
