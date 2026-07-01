
# 🔥 TWO MORE POWER PATTERNS FOR YOUR DEVIN PRESENTATION
## Part A: Preventing Duplicate Research Across Your Team
## Part B: Using GitHub Copilot Alongside Devin (Web-Only Access)

---

# PART A: PREVENTING DUPLICATE RESEARCH ACROSS YOUR TEAM

## THE PROBLEM YOU DESCRIBED

**Developer A (You):**
1. Opened a Devin session
2. Did extensive research to investigate an issue
3. Exchanged 20+ messages with Devin
4. Created an implementation plan
5. Created a new Devin session for implementation
6. PR merged and closed

**Developer B (Teammate):**
1. Opened a Devin session
2. Did THE SAME extensive research
3. Exchanged THE SAME 20+ messages
4. Created THE SAME implementation plan
5. Did the same work all over again

**WASTE:** Same research × same ACUs × same time = Team-wide inefficiency

---

## THE SOLUTION: THE "RESEARCH → KNOWLEDGE → PLAYBOOK" PIPELINE

Devin DOES have features to solve this — but they require a deliberate pattern. Here's the complete system:

---

### STEP 1: SESSION INSIGHTS — EXTRACT LEARNINGS FROM YOUR SESSION

**What It Is:**
Session Insights is an analysis feature that examines your completed sessions to identify patterns, issues, and opportunities. It provides actionable recommendations for improvement.

**Source:** Devin Documentation — Session Insights
https://docs.devin.ai/product-guides/session-insights

**How to Use It:**
After your research session completes, click the **"Session Insights"** button in the top bar of your session. Devin analyzes:
- What research paths were explored
- What dead ends were hit
- What the final solution was
- What could have been done better

**What You Get:**
- **Issue Timeline:** Chronological view of what happened (color-coded: Red=high impact issue, Yellow=medium, Green=value provided)
- **Actionable Feedback:** Improved prompt suggestions + action items for your environment
- **Pattern Recognition:** Why Devin chose certain approaches over alternatives

**Example Prompt to Devin:**
```
"Analyze this session where I investigated the payment timeout issue.
Extract the key findings, the root cause, the solution approach,
and any patterns that would help another developer facing the same issue."
```

---

### STEP 2: TURN SESSION INTO KNOWLEDGE — SHARE THE LEARNINGS

**What It Is:**
Knowledge is a collection of tips, advice, and instructions that Devin references across ALL sessions in your organization. Devin automatically recalls relevant Knowledge when needed.

**Source:** Devin Documentation — Knowledge
https://docs.devin.ai/product-guides/knowledge

**How to Create From Your Session:**
After analyzing your session, ask Devin:
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

**Where It Goes:**
- **Organization Knowledge** — Visible to ALL members of your organization
- **Enterprise Knowledge** — Visible across ALL organizations in your enterprise (if you have enterprise)

**Key Settings:**
- **Trigger Description:** Highly specific so Devin retrieves it at the right time
  - Example: `repo:acme-web AND (payment OR timeout OR stripe)`
- **Pin to Repo:** Pin to `acme-web` so it's ALWAYS loaded when working in that repo
- **Macro:** Assign `!payment-timeout-fix` for instant reference

**What Happens Next:**
When Developer B starts a session and mentions "payment timeout" or "stripe errors," Devin AUTOMATICALLY retrieves this Knowledge item. No duplicate research needed.

---

### STEP 3: TURN SESSION INTO PLAYBOOK — CREATE A REUSABLE TEMPLATE

**What It Is:**
Playbooks are reusable templates that guide Devin through specific task types. You can turn a successful session directly into a playbook.

**Source:** Devin Documentation — Advanced Capabilities (Playbooks from Sessions)
https://docs.devin.ai/work-with-devin/advanced-capabilities

**How to Create From Your Session:**
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

**What Devin Does:**
Devin analyzes the session history, identifies the successful pattern, and produces a structured playbook with:
- Procedure section
- Specifications
- Advice
- Forbidden actions
- Required from user

**Assign a Macro:**
`!payment-investigation` — any developer types this and gets your entire research distilled into a template.

**Result:**
Developer B doesn't research. They attach the playbook and Devin follows YOUR proven path.

---

### STEP 4: SCHEDULED KNOWLEDGE MAINTENANCE — KEEP IT FRESH

**What It Is:**
Set up a recurring Devin session to maintain your Knowledge base — deduplicate, resolve conflicts, and fill gaps.

**Source:** Devin Documentation — Scheduled Sessions
https://docs.devin.ai/product-guides/scheduled-sessions

**How to Set Up:**
```
"Create a schedule that runs every Monday at 8 AM to:
1. Review all knowledge entries for duplicates
2. Merge similar entries
3. Resolve conflicting guidance
4. Identify gaps where multiple developers hit the same issue but no knowledge exists"
```

**Where:** Settings > Schedules > Create Schedule

**Why This Matters:**
Without maintenance, your Knowledge base becomes a mess. With maintenance, it becomes a compounding asset.

---

### STEP 5: SLACK INTEGRATION — SHARE SESSIONS IN REAL-TIME

**What It Is:**
When you start a session from the web app, you can "send to channel" to mirror it in Slack. Anyone in the channel can follow along and collaborate.

**Source:** Cognition Blog — December '24 Product Update (Slack Integration)
https://cognition.ai/blog/dec-24-product-update

**How to Use:**
1. Start your research session in Devin web
2. Click "Send to channel" 
3. Select #dev-team or #incidents
4. Your entire session is mirrored in Slack

**What Your Teammates See:**
- Real-time updates on what Devin is doing
- The research path you're taking
- The findings as they emerge
- The final solution

**Result:**
Developer B sees your session in Slack BEFORE they start their own. They can:
- Follow your research instead of duplicating it
- Add context if they know something you don't
- Wait for your PR instead of starting fresh

---

### STEP 6: REPO KNOWLEDGE — AUTO-GENERATED FROM YOUR CODEBASE

**What It Is:**
Devin automatically scans your repositories and generates Repo Knowledge — understanding of your codebase structure, components, and patterns. This is shared across ALL sessions in your organization.

**Source:** Cognition Blog — December '24 Product Update (Repo Knowledge)
https://cognition.ai/blog/dec-24-product-update

**How It Helps:**
- When Developer B starts a session, Devin ALREADY knows your codebase
- No need to re-explain architecture, file structure, or conventions
- The "exploration" phase is dramatically shortened

**Where to Find:**
Settings & Library > Knowledge > Repo Knowledge

---

### THE COMPLETE PIPELINE VISUALIZED

```
┌─────────────────────────────────────────────────────────────────────┐
│  DEVELOPER A's RESEARCH SESSION                                     │
│  (Investigates payment timeout issue, 15 messages, 8 ACUs)         │
└──────────────────────┬──────────────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────────────┐
│  STEP 1: SESSION INSIGHTS                                           │
│  → Analyze what worked, what didn't, patterns extracted             │
└──────────────────────┬──────────────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────────────┐
│  STEP 2: CREATE KNOWLEDGE                                           │
│  → "Payment Timeout Investigation" — org-wide, pinned to repo       │
│  → Trigger: repo:acme-web AND (payment OR timeout)                  │
│  → Macro: !payment-timeout-fix                                      │
└──────────────────────┬──────────────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────────────┐
│  STEP 3: CREATE PLAYBOOK                                            │
│  → "Payment Issue Investigation" — reusable template                │
│  → Macro: !payment-investigation                                    │
└──────────────────────┬──────────────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────────────┐
│  STEP 4: SHARE TO SLACK                                             │
│  → Session mirrored in #dev-team channel                            │
│  → Teammates see the entire research path                           │
└──────────────────────┬──────────────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────────────┐
│  DEVELOPER B encounters same issue                                  │
│  → Devin auto-retrieves Knowledge "Payment Timeout Investigation"   │
│  → Devin suggests: "Use !payment-investigation playbook"            │
│  → Developer B attaches playbook, Devin follows proven path         │
│  → ACUs saved: ~6 (no research needed)                              │
│  → Time saved: ~45 minutes                                          │
└─────────────────────────────────────────────────────────────────────┘
```

---

### THE "GOLDEN RULE" FOR TEAM KNOWLEDGE

> **"Every session that involves research MUST produce either Knowledge or a Playbook. No exceptions."**

**Enforcement:**
- Add this to your team's Definition of Done for Devin sessions
- Make it part of your sprint retrospective: "What Knowledge did we create this sprint?"
- Track it: How many Knowledge items per developer per week?

---

# PART B: USING GITHUB COPILOT ALONGSIDE DEVIN (WEB-ONLY ACCESS)

## THE REALITY CHECK

**You said:** "We have only Devin web access."

**This means:**
- ❌ No Devin CLI (so no `/handoff` from local to cloud)
- ❌ No Devin IDE extension (so no Cmd+G from VS Code)
- ✅ Devin web app only
- ✅ GitHub Copilot in your IDE

**The Good News:** You can still build a powerful Copilot + Devin hybrid workflow. Here's how.

---

## THE HYBRID WORKFLOW: COPILOT FOR SPEED, DEVIN FOR DEPTH

### PHASE 1: LOCAL EXPLORATION WITH COPILOT (FREE)

**What Copilot Excels At:**
- Inline code suggestions as you type
- Quick function implementations
- Small refactors (rename, extract method)
- Explaining code blocks
- Generating unit tests for single functions
- Chat-based Q&A about your codebase

**What to Do With Copilot:**
```
1. Open your IDE with Copilot enabled
2. Use Copilot Chat to explore the issue:
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
   - Understand dependencies
```

**Cost:** $0 (your Copilot subscription covers this)
**Time:** 10-15 minutes of exploration

---

### PHASE 2: DECISION POINT — COPILOT OR DEVIN?

**Use Copilot when:**
- The fix is in 1-3 files
- You know exactly what needs to change
- It's a pattern you've done before
- You want to stay in flow state
- Time estimate: < 30 minutes

**Use Devin when:**
- The task spans 3+ files
- You need research and investigation
- You need tests, lint, and PR creation
- You want to delegate and walk away
- Time estimate: > 30 minutes
- You need browser automation (OAuth, screenshots)

---

### PHASE 3: HAND OFF TO DEVIN (THE WEB-ONLY PATTERN)

**Since you don't have CLI handoff, you use the "Structured Prompt Transfer":**

**Step 1:** In Copilot Chat, ask:
```
"Summarize the issue, the root cause, and the proposed fix 
for the payment timeout bug. Format it as a structured 
implementation plan."
```

**Step 2:** Copilot generates:
```markdown
## Issue Summary
Payment service times out after 30s on Stripe webhook processing

## Root Cause  
Webhook handler doesn't use async processing, blocking the main thread

## Proposed Fix
1. Make webhook handler async
2. Add background job queue for Stripe events
3. Update tests to cover async behavior
4. Add timeout configuration

## Files to Modify
- app/api/webhooks/stripe.ts
- lib/jobs/payment-jobs.ts (new)
- app/api/webhooks/stripe.test.ts
- config/payment.ts

## Acceptance Criteria
- Webhook responds in < 2s
- Events processed asynchronously
- All tests pass
- No breaking changes to API
```

**Step 3:** Copy this plan and paste into Devin web with a Work-Order Prompt:
```
GOAL
  Fix payment service timeout by making Stripe webhook handler async
  and adding background job processing.

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

**What You Just Did:**
- Used Copilot for FREE exploration and planning (0 ACUs)
- Used Devin for EXECUTION and PR creation (3-5 ACUs)
- Total savings: 5-10 ACUs vs. letting Devin do the research too

---

### PHASE 4: THE "COPILOT DRAFT → DEVIN POLISH" PATTERN

**For smaller tasks where Copilot gets you 80% there:**

**Step 1:** Use Copilot to generate the initial code
```
"Generate an async Stripe webhook handler with background job processing"
→ Copilot generates code in your IDE
```

**Step 2:** Review and refine locally with Copilot
```
"Add error handling for invalid webhook signatures"
"Add rate limiting to prevent abuse"
→ Copilot updates the code
```

**Step 3:** When you hit Copilot's limits (complex testing, multi-file changes, PR creation), switch to Devin:
```
GOAL
  Complete the Stripe webhook handler implementation. I've drafted
  the main handler in app/api/webhooks/stripe.ts. Please:
  1. Review and improve the implementation
  2. Add comprehensive tests in app/api/webhooks/stripe.test.ts
  3. Run lint and typecheck
  4. Open a PR

CONTEXT
  [Paste your Copilot-generated code here]
  [Paste any Copilot chat context about the design decisions]
```

**Result:**
- Copilot did the "thinking" and "drafting" (free)
- Devin did the "testing," "polishing," and "PR" (paid, but minimal ACUs)

---

### PHASE 5: THE "COPILOT FOR QUICK FIXES, DEVIN FOR BACKLOG" SPLIT

**Daily Workflow:**

| Time | Activity | Tool | ACUs |
|------|----------|------|------|
| Morning | Quick bug fix (1 file) | Copilot | 0 |
| Morning | Code review | Copilot | 0 |
| Afternoon | Feature implementation (5+ files) | Devin | 5-8 |
| Afternoon | Test coverage for legacy code | Devin | 3-5 |
| End of day | Dependency audit | Devin (scheduled) | 2 |

**Weekly Workflow:**

| Day | Activity | Tool |
|-----|----------|------|
| Monday | Sprint planning, task breakdown | Copilot + Devin |
| Tuesday-Thursday | Feature development | Copilot (coding) + Devin (PRs) |
| Friday | Code review, documentation | Copilot |
| Friday | Weekly knowledge maintenance | Devin (scheduled) |

---

### THE ACU MATH: COPILOT + DEVIN vs. DEVIN ALONE

**Scenario: Implement a new API endpoint**

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
Copilot: "Generate a user profile endpoint following our existing patterns"
→ Copilot suggests code inline: 0 ACUs

You: Refine in IDE with Copilot suggestions: 0 ACUs

Devin: "I've drafted the user profile endpoint. Please:
1. Add tests following our test patterns
2. Run lint and typecheck
3. Open a PR"
→ Devin tests + lint + PR: 2 ACUs
Total: 2 ACUs ($4-5)
```

**Savings: 6.5 ACUs = $13-14 per task**

---

### THE "KNOWLEDGE BRIDGE" BETWEEN COPILOT AND DEVIN

**Since Copilot and Devin don't directly integrate, you build the bridge:**

**Create a Knowledge item for your team:**
```
Title: "Copilot → Devin Handoff Pattern"
Trigger: repo:acme-web AND task:implementation

Content:
When starting a new implementation task:
1. FIRST use Copilot in IDE to:
   - Explore the codebase
   - Draft initial code
   - Understand existing patterns

2. THEN use Devin for:
   - Multi-file changes
   - Test writing
   - Lint/typecheck enforcement
   - PR creation

3. When handing off to Devin, ALWAYS include:
   - Copilot's analysis/summary
   - Draft code you've written
   - Design decisions made with Copilot
   - Any gotchas Copilot identified
```

**Result:** Your entire team follows the same hybrid pattern, maximizing Copilot (free) and minimizing Devin ACUs.

---

### LIMITATIONS OF WEB-ONLY ACCESS (And Workarounds)

| Limitation | Workaround |
|-----------|-----------|
| No CLI handoff | Use "Structured Prompt Transfer" (copy Copilot analysis into Devin prompt) |
| No IDE extension | Use browser + IDE side-by-side, or use Devin web on second monitor |
| No local file sync | Commit Copilot drafts to a branch, tell Devin to work from that branch |
| No real-time sync | Use GitHub as the bridge — commit Copilot work, Devin picks it up |

---

### THE "BRANCH HANDOFF" TECHNIQUE

**For complex tasks where you want Copilot to start and Devin to finish:**

**Step 1:** In your IDE with Copilot:
```bash
git checkout -b wip/payment-fix-copilot-draft
# Write code with Copilot suggestions
git add .
git commit -m "wip: draft payment fix with copilot"
git push origin wip/payment-fix-copilot-draft
```

**Step 2:** In Devin web:
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
- Copilot did the creative work (free)
- Devin did the mechanical work (minimal ACUs)
- GitHub is the bridge between them

---

## SUMMARY: THE COMPLETE SYSTEM

### For Duplicate Research Prevention:
1. **Session Insights** → Extract learnings from every research session
2. **Knowledge** → Share findings organization-wide with smart triggers
3. **Playbooks** → Turn successful sessions into reusable templates
4. **Slack Integration** → Mirror sessions so teammates can follow along
5. **Scheduled Maintenance** → Keep Knowledge base clean and current
6. **Repo Knowledge** → Auto-generated codebase understanding

### For Copilot + Devin Hybrid (Web-Only):
1. **Copilot for Exploration** → Free research and drafting in IDE
2. **Structured Prompt Transfer** → Copy Copilot analysis into Devin
3. **Copilot Draft → Devin Polish** → Use each tool for what it does best
4. **Branch Handoff** → Use GitHub as the bridge between tools
5. **Knowledge Bridge** → Document the hybrid pattern for your team

### Expected Combined Impact:
- **Duplicate research eliminated:** 80% reduction in repeated investigations
- **ACU savings from Copilot hybrid:** 40-60% reduction in Devin ACUs
- **Team velocity:** 2-3x improvement as knowledge compounds

---

## REFERENCES

### Official Devin Documentation:
- Session Insights: https://docs.devin.ai/product-guides/session-insights
- Knowledge: https://docs.devin.ai/product-guides/knowledge
- Advanced Capabilities (Playbooks from Sessions): https://docs.devin.ai/work-with-devin/advanced-capabilities
- Scheduled Sessions: https://docs.devin.ai/product-guides/scheduled-sessions
- Automations: https://docs.devin.ai/product-guides/automations
- Organizations: https://docs.devin.ai/enterprise/getting-started/organizations

### GitHub Copilot Documentation:
- Copilot Chat: https://docs.github.com/en/copilot/using-github-copilot/copilot-chat
- Copilot in IDE: https://docs.github.com/en/copilot/using-github-copilot/getting-started-with-github-copilot

### Cognition Blog:
- Devin December '24 Product Update (Slack, Repo Knowledge): https://cognition.ai/blog/dec-24-product-update
- Devin CLI & Handoff: https://cognition.ai/blog (search "Devin CLI")

---

*Compiled for enterprise teams using Devin web access + GitHub Copilot. Last updated: June 2026.*
