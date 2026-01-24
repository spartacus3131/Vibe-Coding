# Phase 5: Building

**Build one feature at a time. Demo every 2 weeks. Adjust based on feedback.**

No sprint planning meetings. No daily standups with yourself. Just build, show, learn, repeat.

---

## THE SIMPLE LOOP

```
┌─────────────────────────────────────────┐
│                                         │
│   Build Feature (TDD)                   │
│         ↓                               │
│   Push → Tests Run → Staging Deploys    │
│         ↓                               │
│   Feature Done? Mark it passing         │
│         ↓                               │
│   Next Feature                          │
│         ↓                               │
│   Every 2 Weeks: Demo to Stakeholders   │
│         ↓                               │
│   Get Feedback → Adjust Priorities      │
│         ↓                               │
│   Keep Building                         │
│                                         │
└─────────────────────────────────────────┘
```

---

## SETUP (1-2 Hours, Once)

### Step 1: Create feature_list.json

This is your source of truth. Extract features from Phase 2 Bounded Context Canvases.

```json
{
  "project": "Your App Name",
  "created": "2025-01-24",
  "features": [
    {
      "id": "auth-001",
      "name": "User Registration",
      "context": "User Identity",
      "priority": "critical",
      "status": "backlog",
      "passes": false,
      "notes": "Use Auth0, JWT tokens"
    },
    {
      "id": "auth-002", 
      "name": "User Login",
      "context": "User Identity",
      "priority": "critical",
      "status": "backlog",
      "passes": false,
      "notes": "Depends on auth-001"
    },
    {
      "id": "coaching-001",
      "name": "Start Coaching Session",
      "context": "Coaching Conversations",
      "priority": "high",
      "status": "backlog",
      "passes": false,
      "notes": "Core feature"
    }
  ]
}
```

**Priority levels:**
- `critical` - MVP won't work without this
- `high` - Important, build soon
- `medium` - Nice to have
- `low` - Defer until later

### Step 2: Create the AI Plans Directory

**This is Luke's key insight:** Commit not just the code, but the plans that got you there.

Create `ai-plans/` directory:

```
your-project/
├── ai-plans/
│   ├── README.md           # What this directory is for
│   ├── prd.md              # Your Phase 1 PRD
│   ├── domain-model.md     # Your Phase 2 outputs
│   ├── architecture.md     # Your Phase 3 decisions
│   └── decisions/          # Individual decision records
│       ├── 001-auth-choice.md
│       └── 002-database-choice.md
├── src/
├── tests/
└── ...
```

**Why this matters:**

> "Later when you go to build on it or want to make a change, it's a nightmare if you've lost all the context that it took to get there."
> — Luke

### ai-plans/README.md

```markdown
# AI Plans Directory

This directory contains the planning documents and decisions that shaped this codebase.

## Contents

- `prd.md` - Product Requirements Document (Phase 1)
- `domain-model.md` - Event storms, context maps, canvases (Phase 2)
- `architecture.md` - Technical architecture decisions (Phase 3)
- `decisions/` - Individual decision records

## Why This Exists

When you (or an AI) need to make changes later, these documents provide:
- WHY decisions were made
- WHAT tradeoffs were considered
- HOW components relate to each other

Don't delete these. They're as important as the code.
```

### Step 3: Create Progress Log

Create `ai-plans/progress.md`:

```markdown
# Progress Log

## [Date] - Session Notes

**Worked on:** [Feature ID and name]
**Status:** [Done / In Progress / Blocked]
**Notes:** [Anything worth remembering]
**Next:** [What to do next session]

---
```

### Step 4: Create init.sh

```bash
#!/bin/bash
echo "Starting dev environment..."
npm install
npm run dev
echo "Ready at http://localhost:3000"
```

---

## DAILY WORKFLOW

### Morning: Pick a Feature

Look at `feature_list.json`. Find highest priority with status "backlog". That's today's work.

### Build: TDD Loop

```
1. Write failing test for the feature
2. Run test - confirm it fails (red)
3. Write minimum code to pass
4. Run test - confirm it passes (green)
5. Refactor if needed
6. Run ALL tests - confirm nothing broke
7. Commit
```

### End of Day: Update

```bash
# Update feature_list.json
# - status: "backlog" → "in-progress" or "done"
# - passes: true if tests pass

# Update ai-plans/progress.md
# - What you did
# - Any blockers
# - What's next

# Commit
git add .
git commit -m "feat: [feature-id] [brief description]"
git push
```

Push triggers CI/CD → Tests run → Staging deploys automatically.

---

## EVERY 2 WEEKS: STAKEHOLDER DEMO

### The Demo (30 minutes)

**Show, don't tell:**
- Open staging environment
- Walk through features built
- Let them click around

**Ask:**
- "Does this work like you expected?"
- "What's missing?"
- "What should we build next?"

**Listen:**
- Write down feedback
- Don't defend—just capture

### After the Demo (15 minutes)

Adjust `feature_list.json` based on feedback:

```json
{
  "id": "auth-003",
  "name": "Password Reset",
  "priority": "critical",  // Elevated from medium
  "status": "backlog",
  "notes": "Added based on stakeholder feedback 2025-01-24"
}
```

### No Stakeholders?

Demo to yourself every 2 weeks:
- Use the product as a real user would
- Ask: "Is this actually solving my problem?"

---

## DECISION RECORDS

When you make a significant decision, document it.

Create `ai-plans/decisions/XXX-decision-name.md`:

```markdown
# Decision: [Title]

**Date:** [Date]
**Status:** Accepted

## Context

[What situation led to this decision?]

## Decision

[What did you decide?]

## Consequences

[What are the implications?]

## Alternatives Considered

[What else did you consider and why not?]
```

**Example:**

```markdown
# Decision: Use Supabase for Database

**Date:** 2025-01-24
**Status:** Accepted

## Context

Need a database for user data, coaching sessions, and AI conversation history.
Solo founder, want to minimize DevOps overhead.

## Decision

Use Supabase (PostgreSQL) with Row Level Security.

## Consequences

- Get auth, database, and edge functions in one platform
- Locked into Supabase ecosystem
- PostgreSQL is portable if we need to migrate

## Alternatives Considered

- **PlanetScale (MySQL)**: Good, but no built-in auth
- **Firebase**: NoSQL didn't fit our relational needs
- **Self-hosted Postgres**: Too much DevOps for solo founder
```

---

## FEATURE STATES

```
backlog → in-progress → done
                ↓
            blocked (if stuck)
```

| State | Meaning |
|-------|---------|
| `backlog` | Not started |
| `in-progress` | Currently building |
| `done` | Tests pass, deployed to staging |
| `blocked` | Can't proceed (document why) |

---

## WHEN YOU'RE BLOCKED

**Can't figure out how to build something?**
1. Check Phase 2 canvas—is the domain clear?
2. Check Phase 3 architecture—is the approach clear?
3. Ask Claude to explain the concept
4. Prototype it in isolation first

**Waiting on external dependency?**
1. Mark feature as "blocked" with reason
2. Move to next feature
3. Come back when unblocked

**Everything is hard?**
1. Take a break
2. Go back to Phase 2/3—maybe design is wrong
3. Ask for help

---

## DONE CRITERIA

A feature is DONE when:

- [ ] Tests written and passing
- [ ] Code committed and pushed
- [ ] CI/CD pipeline passed
- [ ] Deployed to staging
- [ ] Manually tested in staging
- [ ] `feature_list.json` updated: `"passes": true`

**Not done until deployed to staging and tested.** Local-only doesn't count.

---

## PROJECT COMPLETE

You're done when:

- [ ] All features in `feature_list.json` have `"passes": true`
- [ ] All tests pass
- [ ] Deployed to production
- [ ] Stakeholders approve (if applicable)

---

## FILE STRUCTURE

```
project/
├── ai-plans/
│   ├── README.md              # What this directory is for
│   ├── prd.md                 # Phase 1 PRD
│   ├── domain-model.md        # Phase 2 outputs
│   ├── architecture.md        # Phase 3 decisions
│   ├── progress.md            # Session log
│   └── decisions/             # Decision records
├── feature_list.json          # Source of truth for features
├── init.sh                    # Dev environment startup
├── .github/workflows/         # CI/CD from Phase 4.5
├── src/                       # Your code
└── tests/                     # Your tests
```

---

## QUICK REFERENCE

| Task | Action |
|------|--------|
| Start building | Pick highest priority backlog feature |
| Build feature | TDD: test → fail → implement → pass → refactor |
| End of day | Update feature_list.json, commit, push |
| Every 2 weeks | Demo to stakeholders, get feedback |
| Make decision | Document in ai-plans/decisions/ |
| Done | All features passing, deployed to production |

---

## COMPLETION CRITERIA

Project is complete when:

- [ ] All features in feature_list.json passing
- [ ] All tests pass
- [ ] Deployed to production
- [ ] ai-plans/ directory committed with all decisions
- [ ] Stakeholders have approved

---

**You're a solo builder. Build, show, learn, repeat. That's the whole system.**
