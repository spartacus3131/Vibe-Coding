# Vibe Coding Guide v3

**A complete framework for building products with AI coding tools**

Based on analysis of real codebases and Luke transcript insights.

---

## What's New in v3

### 1. Base + Extension Model for Requirements

Instead of separate PRD vs GPRD documents, we now have:

- **Base PRD** - Always use this. Covers all products.
- **AI Extension** - Add ONLY when you have AI-GENERATIVE features

### 2. Three Types of AI Features

| Type | Description | Treatment |
|------|-------------|-----------|
| **DETERMINISTIC** | Traditional code | Base PRD only |
| **AI-UTILITY** | AI trying to be accurate (transcription, OCR) | Base PRD only |
| **AI-GENERATIVE** | AI with designed variability (chatbots, content) | Base PRD + AI Extension |

### 3. Consolidated Phase 2 Documents

Event Storming, Context Mapping, and Bounded Context Canvas now have unified templates with `[AI-POWERED]` sections that activate only when needed.

### 4. Ready-to-Use Rules

Copy these directly to `.cursor/rules/`:

- **Universal rules** (6) - TDD, documentation, dependencies, git, errors, improvement
- **Stack templates** (5) - TypeScript, React/Next.js, Python/FastAPI, Supabase, Claude
- **Project templates** (4) - Domain language, bounded contexts, state machines, AI behavior

### 5. AI Plans Concept

From Luke: "Commit not just the code, but the plans that got you there."

Phase 5 now includes an `ai-plans/` directory structure to preserve context.

---

## File Structure

```
vibe-coding-guide-v3/
├── pm-orchestrator-v3.md                    # START HERE
│
├── phase-1/                                 # Product Requirements
│   ├── pm-phase-1-requirements-base.md      # ALL products
│   └── pm-phase-1-requirements-ai-extension.md  # Add for AI-GENERATIVE
│
├── phase-2/                                 # Domain Architecture
│   ├── pm-phase-2a-event-storming.md        # Map events
│   ├── pm-phase-2b-context-mapping.md       # Identify contexts
│   └── pm-phase-2c-bounded-context-canvas.md    # Detail each context
│
├── phase-3/                                 # Technical Architecture
│   └── pm-phase-3-technical-architecture.md # Stack decisions
│
├── phase-4.5/                               # DevOps (Optional)
│   └── pm-phase-4.5-devops.md               # CI/CD setup
│
├── phase-5/                                 # Building
│   └── pm-phase-5-building.md               # Feature-by-feature + AI Plans
│
├── rules/
│   ├── universal/                           # Copy as-is
│   │   ├── 001-tdd.mdc
│   │   ├── 002-documentation.mdc
│   │   ├── 003-dependencies.mdc
│   │   ├── 004-git.mdc
│   │   ├── 005-error-handling.mdc
│   │   └── 006-continuous-improvement.mdc
│   │
│   ├── stack-templates/                     # Customize for your stack
│   │   ├── typescript.mdc
│   │   ├── react-nextjs.mdc
│   │   ├── python-fastapi.mdc
│   │   ├── supabase.mdc
│   │   └── ai-claude.mdc
│   │
│   └── project-templates/                   # Customize for your domain
│       ├── domain-language.mdc
│       ├── bounded-contexts.mdc
│       ├── state-machines.mdc
│       └── ai-behavior.mdc
│
└── reference/
    └── glossary-for-non-coders.md           # Plain English tech terms
```

---

## How to Use This (Step by Step)

Each phase document is designed to be **loaded directly into your AI coding tool** (Cursor, Claude Code, etc.). You paste the document into a conversation, describe your product, and the AI walks you through filling out the templates.

### Phase 1: Product Requirements (2-4 hours)

> **Goal:** Define WHAT you're building and WHY. No technology decisions.

1. Open a new AI chat session
2. Paste the contents of `pm-orchestrator-v3.md` — this gives the AI the full picture
3. Paste the contents of `phase-1/pm-phase-1-requirements-base.md`
4. Tell the AI about your product idea and work through the template together:
   - Answer the 4 W's (Who, What, Why, Where)
   - Write Sad/Happy user stories
   - Document current workflow
   - Define MVP scope, success metrics, and user flows
   - Classify your features: **DETERMINISTIC** / **AI-UTILITY** / **AI-GENERATIVE**
5. **If you have AI-GENERATIVE features:** Also load `phase-1/pm-phase-1-requirements-ai-extension.md` and complete it
6. Save the completed PRD to your project repo

### Phase 2: Domain Architecture (3-6 hours)

> **Goal:** Map everything that HAPPENS in your product and organize it into bounded contexts.

Phase 2 has three sub-steps, done in order. For each one, start a new AI chat session with the orchestrator + your completed Phase 1 PRD for context.

**Step 2A — Event Storming:**
1. Load `phase-2/pm-phase-2a-event-storming.md` along with your completed PRD
2. For each user flow from your PRD, map out: events, commands, actors, and policies
3. If you have AI features, label each event `[DETERMINISTIC]` or `[AI-POWERED]`

**Step 2B — Context Mapping:**
1. Load `phase-2/pm-phase-2b-context-mapping.md` along with your event storm output
2. Group your events into bounded contexts (subdomains)
3. Map the relationships between contexts

**Step 2C — Bounded Context Canvas:**
1. Load `phase-2/pm-phase-2c-bounded-context-canvas.md` along with your context map
2. Complete a canvas for EVERY bounded context — entities, rules, interfaces

### Phase 3: Technical Architecture (4-8 hours)

> **Goal:** Make technology decisions that fit your product, then validate risky ones.

1. Start a new AI chat session with the orchestrator + your completed Phase 1 and Phase 2 docs
2. Load `phase-3/pm-phase-3-technical-architecture.md`
3. Work through these decisions with the AI:
   - **Stack decisions:** Frontend, backend, database, auth, hosting (with rationale)
   - **Infrastructure:** Monolith vs. modular vs. microservices
   - **Data architecture:** Map every entity from Phase 2 to database storage
   - **State machines:** Define states and transitions for stateful entities
4. **Risk prototyping (2-4 hours):** For each complexity flag from Phase 1, build a minimal prototype with real APIs (not mocks) and document what you learned
5. Save the completed architecture doc to your project repo

### After Phase 3

Continue with the orchestrator through Phases 4 (Cursor Rules), 4.5 (DevOps), and 5 (Building). The same pattern applies — load the phase doc, work through it with AI, save the output.

---

## Key Insight from Real-World Analysis

In a typical AI-powered product codebase:
- **95%** is DETERMINISTIC (auth, storage, UI, CRUD)
- **~5%** is AI (e.g., a single generative edge function)

That 5% AI is the **core value proposition**, but it's cleanly separated. This validates the Base + Extension approach:
- Don't pollute deterministic thinking with AI concerns
- Don't skip AI concerns for generative features

---

## What's Included

### Phase Documents (9)
| Phase | Document | Purpose |
|-------|----------|---------|
| 1 | Base PRD | Define WHAT and WHY (all products) |
| 1 | AI Extension | Add AI behavior specs (generative only) |
| 2A | Event Storming | Map domain events |
| 2B | Context Mapping | Identify bounded contexts |
| 2C | Bounded Context Canvas | Detail each context |
| 3 | Technical Architecture | Stack and data decisions |
| 4.5 | DevOps | CI/CD setup |
| 5 | Building | Feature-by-feature workflow |

### Rules (15)
| Category | Count | Files |
|----------|-------|-------|
| Universal | 6 | TDD, docs, deps, git, errors, improvement |
| Stack Templates | 5 | TypeScript, React, Python, Supabase, Claude |
| Project Templates | 4 | Domain language, contexts, state machines, AI behavior |

---

## Time Estimates

| Phase | Time |
|-------|------|
| Phase 1 | 2-4 hours |
| Phase 2 | 3-6 hours |
| Phase 3 | 4-8 hours (includes prototyping) |
| Phase 4 | 2-4 hours |
| Phase 4.5 | 30-60 minutes |
| Phase 5 | Ongoing (~30-90 min per feature) |

**Total before building:** 12-24 hours of planning
