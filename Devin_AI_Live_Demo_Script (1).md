
# 🎬 LIVE DEMO SCRIPT: Showcasing Devin Power Features
## Follow this script during your presentation demo

---

## DEMO 1: WORK-ORDER PROMPTING (5 minutes)

### Setup Before Demo
- Open a Devin session
- Have your "Add API Endpoint" playbook ready
- Have a simple task prepared (e.g., "Add a health check endpoint")

### Script

**[YOU]:** "Let me show you the difference between how I used to prompt Devin and how I do it now."

**[ACTION]:** Show a screenshot or recording of an OLD vague prompt:
```
'fix the auth bug'
```
**[YOU]:** "This is what I used to do. Vague, no context, no boundaries. Devin would explore for an hour, refactor files I never asked for, and burn 6 ACUs."

**[ACTION]:** Now show the Work-Order Prompt:
```
GOAL
  Add a /health endpoint that returns { status: 'ok', timestamp: ISOString }

CONTEXT
  Repo: github.com/acme/acme-web (branch: demo/health-endpoint)
  Stack: TypeScript, Express, Jest
  Pattern to follow: app/api/status/route.ts

ACCEPTANCE CRITERIA
  1. GET /health returns { status: 'ok', timestamp: <ISO> }
  2. `npm test` passes with new test
  3. `npm run lint` passes
  4. Only app/api/health/ files are modified

SCOPE
  In scope: health route + test file
  Out of scope: any other route, dependencies, schema

ENVIRONMENT
  Install: npm ci
  Test: npm test
  Lint: npm run lint

CLOSING STEP
  Open PR titled "feat: add health check endpoint"
  Do not merge
```

**[YOU]:** "Watch what happens. Devin doesn't explore. It doesn't refactor random files. It follows the recipe."

**[ACTION]:** Let Devin execute (or show a pre-recorded session)
**[YOU]:** "Done in 2 ACUs instead of 6. And the PR is exactly what I asked for."

---

## DEMO 2: PLAYBOOK MACROS (3 minutes)

### Setup Before Demo
- Have your playbook with macro `!add-endpoint` configured
- Have the macro ready to trigger

### Script

**[YOU]:** "Now let me show you Playbook Macros. Instead of copy-pasting that entire prompt every time..."

**[ACTION]:** Type in the prompt box:
```
!add-endpoint for /health, public access
```

**[YOU]:** "That's it. The entire playbook loads instantly. Devin knows exactly what to do because I've refined this playbook over 20 sessions."

**[ACTION]:** Show the playbook loading with the blue pill indicator
**[YOU]:** "See that blue pill? That's the playbook attached. Every developer on our team gets the same high-quality prompt, every time."

---

## DEMO 3: MANAGED DEVINS / PARALLEL EXECUTION (5 minutes)

### Setup Before Demo
- Prepare a multi-file task (e.g., "Add logging to all API endpoints")
- Have the coordinator prompt ready

### Script

**[YOU]:** "This is the feature that changed everything for me. Watch this."

**[ACTION]:** Start a new session and type:
```
"Analyze our codebase for all files in app/api/ that don't have 
structured logging. Group them into independent work packages 
that won't conflict, then start a parallel Devin session for each 
package to add structured logging using our winston logger from 
lib/logger.ts. Use the 'Add Logging' playbook for each session."
```

**[YOU]:** "I'm not asking Devin to do the work. I'm asking Devin to MANAGE the work."

**[ACTION]:** Show the "Agents" tab appearing with child sessions
**[YOU]:** "See these child sessions? Each one is an independent Devin working on its own VM. The coordinator monitors them all."

**[ACTION]:** Show the coordinator monitoring progress
**[YOU]:** "While these run, I can go get coffee. When I come back, I'll have 5 PRs ready for review."

**[YOU]:** "Total ACU cost: about 75% of what sequential would cost, and done in hours instead of days."

---

## DEMO 4: DEVIN REVIEW (3 minutes)

### Setup Before Demo
- Have a recently merged PR ready to show
- Or use a public PR on GitHub

### Script

**[YOU]:** "Let me show you Devin Review. This isn't just 'AI comments on your PR.' This is a full review platform."

**[ACTION]:** Navigate to app.devin.ai/review or use the URL shortcut
**[YOU]:** "I can replace 'github.com' with 'devinreview.com' in any PR URL."

**[ACTION]:** Show the smart diff organization
**[YOU]:** "See how it groups related changes together? Not alphabetically like GitHub. Logically."

**[ACTION]:** Show the bug catcher or security scan
**[YOU]:** "It caught a potential SQL injection here that I missed. And look — it even classified it by CWE severity."

**[ACTION]:** Show the codebase-aware chat
**[YOU]:** "I can ask questions about the PR and get answers with context from the entire codebase."

**[YOU]:** "And the best part? Review ACUs don't count against our session limits. It's essentially free quality assurance."

---

## DEMO 5: SESSION INSIGHTS (2 minutes)

### Setup Before Demo
- Have a recent session with insights available

### Script

**[YOU]:** "After every session, I check Session Insights. This is where I learn."

**[ACTION]:** Click "View Session Insights" on a session
**[YOU]:"** See this timeline? It shows exactly where Devin spent time."

**[ACTION]:** Point to a long browser session
**[YOU]:** "Here — Devin spent 20 minutes browsing docs. That means my Knowledge base is missing something. I need to add documentation there."

**[ACTION]:** Point to multiple test failures
**[YOU]:** "Here — three test failure cycles. My acceptance criteria weren't clear enough. I'll refine the playbook."

**[YOU]:** "This feedback loop is what turns a good Devin user into a great one. Every session teaches you something."

---

## DEMO 6: CLI HANDOFF (3 minutes)

### Setup Before Demo
- Have Devin CLI installed and running
- Have a simple task ready to hand off

### Script

**[YOU]:** "Finally, let me show you the CLI handoff pattern."

**[ACTION]:** Open terminal with Devin CLI
```bash
$ devin
> explore the auth module and find where JWT validation happens
```

**[YOU]:** "This is running on MY machine. It's free. No ACUs."

**[ACTION]:** Let it explore and find the issue
```bash
> /handoff fix the JWT validation bug where expired tokens 
  aren't rejected in auth_middleware.rb
```

**[YOU]:** "Now I'm handing off to cloud Devin. It gets my conversation context, my branch, even my uncommitted changes."

**[ACTION]:** Show the cloud session starting
**[YOU]:** "I can close my laptop now. When I come back, there's a PR waiting."

**[YOU]:** "The pattern is: explore locally for free, hand off to cloud when the work gets serious."

---

## DEMO WRAP-UP (1 minute)

**[YOU]:** "So let's recap what we saw:
1. Work-Order Prompting — saves 50-60% ACUs
2. Playbook Macros — instant, consistent quality
3. Managed Devins — parallel execution for multi-file tasks
4. Devin Review — free quality gate
5. Session Insights — continuous improvement
6. CLI Handoff — free exploration, paid execution

These aren't theoretical. I've been using them for 3 months. My ACU consumption dropped 64%. My output tripled.

The question isn't 'Can we afford to invest in setup?' The question is 'Can we afford NOT to?'"

---

*Demo script prepared for live Devin session demonstration. Adjust timing based on your presentation slot.*
