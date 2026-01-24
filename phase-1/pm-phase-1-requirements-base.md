# Phase 1: Product Requirements Document (Base)

**Use this for ALL products.** This covers the universal requirements thinking that applies whether you're building a todo app or an AI agent.

If your product has **generative AI features** (conversation, content creation, AI coaching), also load `pm-phase-1-requirements-ai-extension.md` after completing this document.

---

## CRITICAL RULES - NON-NEGOTIABLE

### NO TECHNOLOGY DECISIONS

You are defining WHAT to build and WHY. You are NOT deciding HOW to build it.

**FORBIDDEN in this phase:**
- Mentioning databases, frameworks, or languages
- Discussing API design
- Making infrastructure decisions
- Writing any code or pseudocode

If you find yourself thinking about technology, STOP. You are in the wrong mindset.

### EVERY TERM MUST BE DEFINED

If you use a domain-specific term, it MUST be in the glossary.

No exceptions. Ambiguous language causes implementation bugs.

### SAD/HAPPY STORIES ARE MANDATORY

Do NOT skip the Sad and Happy user stories. They are your north star.

If your product doesn't transform the Sad story into the Happy story, you are building the wrong thing.

### WHY NOW MUST BE COMPELLING

Products fail as often from bad timing as from bad execution. You must articulate:
- What has changed that makes this possible or necessary now?
- Why not last year? Why not next year?
- What window of opportunity exists?

---

## THE 4 W's

Before writing anything, you MUST be able to answer:

| Question | What You're Answering |
|----------|----------------------|
| **WHO** is affected? | Your specific target user (not "everyone") |
| **WHAT** is the problem? | The concrete pain they experience |
| **WHY** does it matter? | The real impact on their life/work |
| **WHERE** does it happen? | The context and frequency |

If you cannot answer these clearly, you do NOT understand the problem well enough.

---

## PROCESS - FOLLOW THIS ORDER

### Step 1: Answer the 4 W's
Write 1-2 sentences for each. Do NOT proceed until clear.

### Step 2: Write the Sad User Story
A specific person (use a name) suffering from this problem. Make it visceral.

### Step 3: Write the Happy User Story
The SAME person with your product. Show the journey and transformation.

### Step 4: Document the Current Workflow
How do people solve this today? Where does it break?

### Step 5: Extract Core Problems
2-4 specific problems from the workflow. Quantify if possible.

### Step 6: Write the MVP Scope
Checkboxes for exactly what's in v1. Also list what's OUT and why.

### Step 7: Define Success Metrics
2-4 metrics with measurement method and target.

### Step 8: Document User Flows
Step-by-step for each major flow.

### Step 9: Build the Glossary
EVERY domain-specific term defined in plain English.

### Step 10: Identify Technical Risks
Third-party dependencies, complexity flags, scale assumptions.

---

## PRD TEMPLATE

```markdown
# [Product Name] - Product Requirements Document (v1)

**Product:** [Name]
**Owner:** [Your name]
**Status:** [Draft / Ready for Domain Architecture]
**Has Generative AI:** [Yes/No - if Yes, complete AI Extension after this]

---

## Executive Summary

**TL;DR:** [One sentence—what is this product?]

**Problem:** [One sentence—what pain does it solve?]

**Solution:** [One sentence—how does it solve it?]

**Business Model:** [One sentence—how does it make money? Write "TBD" if unknown.]

---

## Why Now

[2-3 sentences: Why build this now? What's changed? What window of opportunity exists?]

---

## User / Persona

**Primary user:** [Specific description—not "everyone"]

**Key characteristics:**
- [Characteristic 1]
- [Characteristic 2]
- [Characteristic 3]

**Technical comfort level:** [Low / Medium / High]

---

## The 4 W's

| Question | Answer |
|----------|--------|
| **WHO** is affected? | [Answer] |
| **WHAT** is the problem? | [Answer] |
| **WHY** does it matter? | [Answer] |
| **WHERE** does it happen? | [Answer] |

---

## Sad User Story

[Narrative paragraph—specific person, real emotion, clear failure. Minimum 5 sentences. Use a name.]

## Happy User Story

[Narrative paragraph—same person with your product. Show the journey and transformation. Minimum 5 sentences.]

---

## Current Workflow (The Problem in Detail)

How do people try to solve this problem today?

1. **[Step name]:** [What they do and what happens]
2. **[Step name]:** [What they do and what happens]
3. **[Step name]:** [Where it breaks down]
4. **[Step name]:** [The unsatisfying result]

**Core Problems:**
- **[Problem 1]:** [Description, quantified if possible]
- **[Problem 2]:** [Description]
- **[Problem 3]:** [Description]

---

## Product Overview

[Product name] is a [type of product] that:
- [Does thing 1]
- [Does thing 2]
- [Does thing 3]

---

## Key Differentiators

Why this wins against alternatives:

- **[Differentiator 1]:** [Why this matters to users]
- **[Differentiator 2]:** [Why this matters to users]
- **[Differentiator 3]:** [Why this matters to users]

---

## Component Classification

Categorize your product's features:

**[DETERMINISTIC] Features:**
Traditional features with predictable behavior.
- [ ] [Feature 1: e.g., User authentication]
- [ ] [Feature 2: e.g., Data storage and retrieval]
- [ ] [Feature 3: e.g., Timer/scheduling]

**[AI-UTILITY] Features (if any):**
AI that aims for "correct" output (transcription, classification, search).
- [ ] [Feature 1: e.g., Voice-to-text transcription]
- [ ] [Feature 2: e.g., Document classification]

**[AI-GENERATIVE] Features (if any):**
AI that produces variable, designed output (conversation, content creation).
- [ ] [Feature 1: e.g., Coaching conversation]
- [ ] [Feature 2: e.g., Content generation]

> **If you have AI-GENERATIVE features, complete the AI Extension document after this.**

---

## MVP Scope

What's included in the first version:

- [ ] [Feature 1—specific and concrete]
- [ ] [Feature 2—specific and concrete]
- [ ] [Feature 3—specific and concrete]
- [ ] [Feature 4—specific and concrete]
- [ ] [Feature 5—specific and concrete]

**Out of Scope (for now):**
- [Thing NOT included and why]
- [Thing NOT included and why]
- [Thing NOT included and why]

---

## Success Metrics

| Metric | How We'll Measure | Target |
|--------|-------------------|--------|
| [Metric 1] | [Measurement method] | [Specific target] |
| [Metric 2] | [Measurement method] | [Specific target] |
| [Metric 3] | [Measurement method] | [Specific target] |

---

## User Flows

### Flow 1: [Name of primary flow]

1. User [action]
2. System [response]
3. User [action]
4. System [response]
5. [Outcome]

### Flow 2: [Name of secondary flow]

1. User [action]
2. ...

---

## Technical Risks

### Third-Party Dependencies

| Service | What It Does | Known Limits | Risk Level |
|---------|-------------|--------------|------------|
| [e.g., Auth0] | [Purpose] | [Limits] | [Low/Med/High] |

### Complexity Flags

Mark areas needing extra attention in Phase 3:

- [ ] **Authentication** - Security-critical
- [ ] **Payments** - Money involved
- [ ] **Real-time features** - WebSocket complexity
- [ ] **AI/LLM integration** - Costs, latency, fallbacks
- [ ] **File uploads** - Storage costs, size limits
- [ ] **Background jobs** - Queue infrastructure
- [ ] **Multi-tenancy** - Data isolation critical

### Scale Assumptions

| Metric | Month 1 | Month 6 | Year 1 |
|--------|---------|---------|--------|
| Users | [?] | [?] | [?] |
| Requests/day | [?] | [?] | [?] |
| Data storage | [?] | [?] | [?] |

---

## Glossary (Ubiquitous Language)

THESE TERMS ARE MANDATORY. Use them exactly as written everywhere.

| Term | Definition |
|------|------------|
| [Term 1] | [Plain English definition] |
| [Term 2] | [Plain English definition] |
| [Term 3] | [Plain English definition] |

---

## Open Questions

- [Unresolved question]
- [Unresolved question]

---

## Next Steps

- [ ] All sections complete
- [ ] Glossary has every domain term
- [ ] Technical risks identified
- [ ] If AI-GENERATIVE features exist → Complete AI Extension
- [ ] Ready for Phase 2: Domain Architecture
```

---

## PHASE 1 BASE COMPLETION CHECKLIST

Do NOT proceed until ALL items are checked:

- [ ] 4 W's answered clearly
- [ ] Sad User Story: specific person, name, emotion, failure moment
- [ ] Happy User Story: same person, journey shown, transformation clear
- [ ] Current Workflow: step-by-step, shows exactly where it breaks
- [ ] Core Problems: 2-4 problems, quantified where possible
- [ ] Product Overview: clear bullets of what it does
- [ ] Key Differentiators: why this beats alternatives
- [ ] Component Classification: features categorized correctly
- [ ] MVP Scope: checkbox list with specific, concrete features
- [ ] Out of Scope: explicit boundaries with reasons
- [ ] Success Metrics: metric + measurement + target for each
- [ ] User Flows: step-by-step for each major flow
- [ ] Technical Risks: dependencies, complexity flags, scale assumptions
- [ ] Glossary: EVERY domain term defined
- [ ] Why Now: compelling timing rationale documented

**If you have AI-GENERATIVE features:**
→ Load `pm-phase-1-requirements-ai-extension.md` and complete it now.

**If NO generative AI:**
→ Proceed to Phase 2: Domain Architecture
