# Vibe Coding Orchestrator v3

**Your guide through the complete process** | Updated January 2026

This orchestrator tells you where you are in the process and what to do next. Load this first when starting any project.

---

## THE COMPLETE PROCESS AT A GLANCE

```
PHASE 1: Product Requirements
├── Base PRD (ALL products) ────────────────────── phase-1/pm-phase-1-requirements-base.md
└── AI Extension (IF generative AI) ────────────── phase-1/pm-phase-1-requirements-ai-extension.md
    ↓
PHASE 2: Domain Architecture  
├── Event Storming ─────────────────────────────── phase-2/pm-phase-2a-event-storming.md
├── Context Mapping ────────────────────────────── phase-2/pm-phase-2b-context-mapping.md
└── Bounded Context Canvases ───────────────────── phase-2/pm-phase-2c-bounded-context-canvas.md
    ↓
PHASE 3: Technical Architecture
└── Stack + Data + State Machines ──────────────── phase-3/pm-phase-3-technical-architecture.md
    ↓
PHASE 4: Cursor Rules
├── Universal (copy as-is) ─────────────────────── rules/universal/*.mdc
├── Stack (customize templates) ────────────────── rules/stack-templates/*.mdc
└── Project (customize templates) ──────────────── rules/project-templates/*.mdc
    ↓
PHASE 4.5: DevOps (optional)
└── CI/CD + Staging ────────────────────────────── phase-4.5/pm-phase-4.5-devops.md
    ↓
PHASE 5: Building
└── Feature-by-Feature ─────────────────────────── phase-5/pm-phase-5-building.md
```

---

## PHASE 1: PRODUCT REQUIREMENTS

### What You're Doing
Defining WHAT you're building and WHY. Zero technology decisions.

### Step 1: Classify Your Components

Before writing anything, categorize your product's features:

| Type | Description | Examples |
|------|-------------|----------|
| **DETERMINISTIC** | Traditional code with predictable output | Auth, CRUD, timers, storage |
| **AI-UTILITY** | AI trying to be "correct" | Transcription, OCR, classification, search |
| **AI-GENERATIVE** | AI with designed variability | Chatbots, content generation, coaching |

### Step 2: Complete the Right Documents

**Everyone:** Complete `pm-phase-1-requirements-base.md`

**If you have AI-GENERATIVE components:** Also complete `pm-phase-1-requirements-ai-extension.md`

### How to Know You're Done

**Base PRD Checklist:**
- [ ] 4 W's answered (Who, What, Why, Where)
- [ ] Sad and Happy user stories written
- [ ] Current workflow documented
- [ ] Components classified
- [ ] MVP scope defined with checkboxes
- [ ] Success metrics with targets
- [ ] User flows step-by-step
- [ ] Technical risks identified
- [ ] Glossary complete

**AI Extension Checklist (if applicable):**
- [ ] 5 C's answered (Capability, Context, Constraints, Coherence, Contingency)
- [ ] AI persona defined
- [ ] Response properties specified (measurable)
- [ ] Guardrails documented
- [ ] Evaluation framework set
- [ ] 3-5 example conversations showing variation
- [ ] Fallback behaviors defined

### Next Step
"Phase 1 complete. Now map what HAPPENS in your product. Load `phase-2/pm-phase-2a-event-storming.md`."

---

## PHASE 2: DOMAIN ARCHITECTURE

### What You're Doing
Discovering your domain model by mapping events, contexts, and boundaries.

### The Three Steps

| Step | Purpose | Output |
|------|---------|--------|
| **Event Storming** | Map everything that HAPPENS | Events, commands, actors, policies |
| **Context Mapping** | Group into bounded contexts | Subdomains, context map, relationships |
| **Canvases** | Detail each context | Entities, rules, interfaces |

### Key Rule for AI Products
- Label events: `[DETERMINISTIC]` or `[AI-POWERED]`
- AI contexts need additional sections: behavior properties, guardrails, example variations

### Documents
- `phase-2/pm-phase-2a-event-storming.md`
- `phase-2/pm-phase-2b-context-mapping.md`  
- `phase-2/pm-phase-2c-bounded-context-canvas.md`

### How to Know You're Done
- [ ] Every user flow event-stormed
- [ ] All events labeled [DETERMINISTIC] or [AI-POWERED]
- [ ] Subdomains identified and classified (Core/Supporting/Generic)
- [ ] Context map drawn with relationships
- [ ] Canvas completed for EVERY context
- [ ] AI contexts have behavior properties and examples

### Next Step
"Phase 2 complete. Now make technology decisions. Load `phase-3/pm-phase-3-technical-architecture.md`."

---

## PHASE 3: TECHNICAL ARCHITECTURE

### What You're Doing
Making technology decisions that fit YOUR product, then validating risky ones.

### The Decision Framework

For every major decision, ask:

1. **Do I have this problem NOW?** (Not hypothetically)
2. **Does my ICP require this?** (Table stakes for your customer type)
3. **What's the cost to add later?** (>1 month retrofit = consider now)

### Key Decisions

| Category | Decide |
|----------|--------|
| **Stack** | Frontend, backend, language, database |
| **Infrastructure** | Monolith vs. modular, hosting |
| **Data** | Schema, relationships, multi-tenancy (if B2B) |
| **State Machines** | Formal definitions for stateful entities |
| **AI (if applicable)** | Provider, streaming, token tracking, fallbacks |

### Risk Prototyping (2-4 hours)

For each complexity flag checked in Phase 1:
- Build smallest possible prototype (30-60 min)
- Test with REAL APIs/services, not mocks
- Document what you learned
- Adjust architecture if needed

### Document
- `phase-3/pm-phase-3-technical-architecture.md`

### How to Know You're Done
- [ ] Stack decisions documented with rationale
- [ ] Data architecture maps all entities to storage
- [ ] State machines formally defined
- [ ] High-risk components prototyped
- [ ] No deal-breakers found

### Next Step
"Phase 3 complete. Now create rules to enforce your architecture."

---

## PHASE 4: CURSOR RULES

### What You're Doing
Creating rules that make AI coding tools follow your architecture consistently.

### Three Categories of Rules

| Category | What | Action |
|----------|------|--------|
| **Universal** | Apply to ALL projects | Copy from `rules/universal/` as-is |
| **Stack** | Specific to your tech choices | Customize from `rules/stack-templates/` |
| **Project** | Specific to your domain | Customize from `rules/project-templates/` |

### Universal Rules (Ready to Use)

Copy these directly to your `.cursor/rules/` directory:

```
rules/universal/
├── 001-tdd.mdc                    # Test-driven development
├── 002-documentation.mdc          # Code documentation
├── 003-dependencies.mdc           # NEVER downgrade deps
├── 004-git.mdc                    # Commit practices
├── 005-error-handling.mdc         # Error handling patterns
└── 006-continuous-improvement.mdc # Rule evolution
```

### Stack Templates (Customize)

Based on Phase 3 decisions, customize these:

```
rules/stack-templates/
├── typescript.mdc
├── react-nextjs.mdc
├── python-fastapi.mdc
├── supabase.mdc
├── ai-claude.mdc
└── ...
```

### Project Templates (Customize)

Based on Phase 2 domain model:

```
rules/project-templates/
├── domain-language.mdc    # Ubiquitous language enforcement
├── bounded-contexts.mdc   # Context separation
├── state-machines.mdc     # State transition rules
└── ai-behavior.mdc        # AI-specific (if applicable)
```

### How to Know You're Done
- [ ] Universal rules copied to project
- [ ] Stack rules customized for your tech
- [ ] Project rules created for your domain
- [ ] Rules tested with a simple task
- [ ] All rules use strong language (MUST, NEVER, FORBIDDEN)

### Next Step
"Phase 4 complete. Set up CI/CD (`phase-4.5/pm-phase-4.5-devops.md`) or start building (`phase-5/pm-phase-5-building.md`)."

---

## PHASE 4.5: DEVOPS (Optional)

### What You're Doing
Setting up automated testing and deployment.

### Skip This If
- Just prototyping (no real users yet)
- Will add later when ready to ship

### What You Get
- Push code → tests run automatically
- Tests pass → staging deploys automatically  
- Production deploys with one click
- Rollback in 30 seconds

### Document
- `phase-4.5/pm-phase-4.5-devops.md`

---

## PHASE 5: BUILDING

### What You're Doing
Building features one at a time with feedback loops.

### The Simple Loop

```
Pick highest priority feature from feature_list.json
    ↓
Write test (red)
    ↓
Implement (green)
    ↓
Refactor
    ↓
Commit and push
    ↓
Tests run automatically
    ↓
Update feature_list.json (mark passing)
    ↓
Every 2 weeks: Demo to stakeholders
    ↓
Get feedback → Adjust priorities
    ↓
Repeat
```

### Key Files
- `feature_list.json` - Source of truth for features
- `claude-progress.txt` - Session notes and learnings
- `init.sh` - Dev environment startup

### Document
- `phase-5/pm-phase-5-building.md`

### You're Done When
- All features in feature_list.json have `"passes": true`
- All tests pass
- Deployed to production
- Stakeholders approve

---

## QUICK REFERENCE

### What Document Do I Need?

| I want to... | Load this |
|--------------|-----------|
| Start a new project | This orchestrator |
| Write requirements | `pm-phase-1-requirements-base.md` |
| Add AI to my PRD | `pm-phase-1-requirements-ai-extension.md` |
| Map domain events | `pm-phase-2-event-storming.md` |
| Define bounded contexts | `pm-phase-2-context-mapping.md` |
| Detail one context | `pm-phase-2-bounded-context-canvas.md` |
| Choose tech stack | `pm-phase-3-technical-architecture.md` |
| Get Cursor rules | `rules/universal/` (copy), then templates |
| Set up CI/CD | `pm-phase-4.5-devops.md` |
| Start building | `pm-phase-5-building.md` |

### Time Estimates

| Phase | Time | Notes |
|-------|------|-------|
| Phase 1 (Base) | 2-3 hours | |
| Phase 1 (AI Extension) | 1-2 hours | Only if generative AI |
| Phase 2 | 3-6 hours | Depends on complexity |
| Phase 3 | 4-8 hours | Includes 2-4h prototyping |
| Phase 4 | 1-2 hours | Mostly copy + customize |
| Phase 4.5 | 30-60 min | One-time setup |
| Phase 5 | Ongoing | ~30-90 min per feature |

**Total before building:** 12-20 hours of thinking → then you build FAST

---

## STATUS CHECK

Not sure where you are? Fill this out:

```
Project: _______________
Has AI-GENERATIVE components: [Yes/No]

Phase 1:
  Base PRD complete?        [Yes/No]
  AI Extension complete?    [Yes/No/N/A]

Phase 2:
  Event storms done?        [Yes/No]
  Context map done?         [Yes/No]
  All canvases done?        [Yes/No]

Phase 3:
  Stack decisions made?     [Yes/No]
  Data architecture done?   [Yes/No]
  State machines defined?   [Yes/No]
  Risk prototypes done?     [Yes/No]

Phase 4:
  Universal rules copied?   [Yes/No]
  Stack rules customized?   [Yes/No]
  Project rules created?    [Yes/No]

Phase 4.5:
  CI/CD set up?            [Yes/No/Skipping]

Phase 5:
  feature_list.json exists? [Yes/No]
  Features remaining:       [X of Y]
```

**The first incomplete item is where you should be working.**
