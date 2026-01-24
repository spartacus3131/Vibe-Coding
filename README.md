# Vibe Coding Guide v3

**A complete framework for building products with AI coding tools**

Based on analysis of real codebases (Clairu) and Luke transcript insights.

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

## Quick Start

1. **Load the orchestrator:** `pm-orchestrator-v3.md`
2. **Classify your components:** DETERMINISTIC / AI-UTILITY / AI-GENERATIVE
3. **Complete Phase 1:** Base PRD (+ AI Extension if needed)
4. **Follow the orchestrator** through remaining phases

---

## Key Insight from Clairu Analysis

In the Clairu codebase:
- **95%** is DETERMINISTIC (auth, storage, UI, CRUD)
- **~5%** is AI (one edge function: `coach-reply`)

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
