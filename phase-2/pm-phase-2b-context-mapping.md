# Phase 2B: Context Mapping

**Group events into subdomains, classify them, define bounded contexts, and map relationships.**

Load this AFTER completing Event Storming (Phase 2A).

---

## CRITICAL RULES

### EVENT STORMING MUST BE COMPLETE FIRST

You need the events list as input. If incomplete, STOP and go finish it.

### NO TECHNOLOGY DECISIONS

Context Mapping is about organizing your BUSINESS DOMAIN.

**FORBIDDEN:**
- Microservices decisions
- Database schemas
- API boundaries
- Service architecture

These are technical decisions. They come LATER in Phase 3.

### CORE DOMAINS MUST BE IDENTIFIED

You MUST classify each subdomain as Core, Supporting, or Generic. This determines where you invest effort.

### INTERFACES MUST BE EXPLICIT

For each bounded context, define:
- What it NEEDS from other contexts
- What it EXPOSES to other contexts

Vague boundaries cause tangled systems.

---

## CONCEPTS

### Subdomain
A business problem area. It exists in reality, whether or not you build software.

**How to find them:** Look at your event storm. Group related events together. Ask: "What business area are these events about?"

### Bounded Context
A solution boundary you DESIGN around a subdomain. Within that boundary, one specific model and vocabulary applies consistently.

**Key insight:** Different bounded contexts CAN use the same word to mean different things. The boundaries prevent confusion.

### Core vs Supporting vs Generic

| Type | What It Is | Investment Level |
|------|------------|------------------|
| **CORE** | Your competitive advantage. Why users choose YOU. | Build custom, iterate constantly, measure obsessively |
| **SUPPORTING** | Necessary for core to work. Not differentiating alone. | Build it, but don't over-engineer |
| **GENERIC** | Solved problem (auth, payments, email). | DO NOT build custom. Buy or use libraries. |

**Example:** For a productivity coaching app:
- **Core:** AI coaching experience (this IS the product)
- **Supporting:** User history, progress tracking
- **Generic:** Authentication, notifications

---

## PROCESS

### Step 1: Group Events into Subdomains

Take your master events list from Event Storming. Group related events together.

Ask: "What business area is this event about?"

### Step 2: Classify Each Subdomain

For each subdomain:
- "Is this why customers choose us?" → **CORE**
- "Is this necessary but not differentiating?" → **SUPPORTING**
- "Is this a solved problem?" → **GENERIC**

Be honest. Most products have 1-2 core subdomains, not 5.

### Step 3: Define Bounded Context Boundaries

For each subdomain, decide: Is this one bounded context, or should it be split/combined?

Usually 1:1 for simple products.

### Step 4: Define What Each Context Owns

For each context:
- Responsibilities that belong ONLY to this context
- Data this context is source of truth for
- Decisions this context makes

### Step 5: Define Interfaces

For each context:
- **NEEDS FROM** other contexts (data/capabilities required)
- **EXPOSES TO** other contexts (data/capabilities provided)

### Step 6: Draw the Context Map

Show all contexts, arrows for relationships, what's exchanged.

### Step 7: Validate Boundaries

Check each context:
- Clear, single purpose?
- No overlap with other contexts?
- Can evolve independently?

---

## [AI-POWERED] ADDITIONAL CONSIDERATIONS

If your product has AI-GENERATIVE features:

### AI Capabilities Are Usually CORE

For AI-native products, the AI behavior/interaction is usually your Core subdomain.

Don't accidentally classify it as Supporting just because "it's AI."

Ask: "Is the AI experience why users choose us?" If yes, it's **CORE**.

### Separate AI Experience from AI Infrastructure

| Subdomain | Type | Why |
|-----------|------|-----|
| AI Interaction (conversation, generation) | Core | The experience users pay for |
| Context Management (user history, preferences) | Supporting | Data that makes AI better |
| AI Infrastructure (model APIs, prompt delivery) | Generic | Use existing solutions |

### Common AI-Native Bounded Contexts

| Context | What It Owns | Typical Classification |
|---------|--------------|------------------------|
| AI Conversation/Generation | The AI interaction experience | Core |
| User Context | User profile, preferences, history | Supporting |
| Domain Knowledge | RAG content, reference data | Supporting |
| Evaluation | Quality measurement, metrics | Supporting or Generic |
| Safety/Moderation | Guardrails, content filtering | Supporting |
| User Identity | Auth, accounts | Generic |
| Notifications | Alerts, reminders | Generic |

### AI Data Flow

Document how information flows to and from AI contexts:

**Inputs to AI Context:**
| From Context | What's Provided | Purpose |
|--------------|-----------------|---------|
| User Context | Recent history | Personalization |
| Domain Knowledge | Reference data | Grounding |

**Outputs from AI Context:**
| To Context | What's Provided | Format |
|------------|-----------------|--------|
| User Context | Extracted intents | Structured event |
| Conversation Store | Generated responses | Message object |

---

## TEMPLATES

### Subdomain Identification

```markdown
## Subdomains

### Subdomain: [Name]

**Events in this subdomain:**
- [Event 1] [DETERMINISTIC/AI-POWERED]
- [Event 2]
- [Event 3]

**Business description:** [What business problem area this covers]

**Classification:** Core / Supporting / Generic

**Rationale:** [Why this classification]
```

### Context Map

```markdown
## Bounded Contexts

| Context Name | Subdomain(s) | Type | Purpose | AI Involvement |
|--------------|--------------|------|---------|----------------|
| [Name] | [Subdomain] | Core/Supporting/Generic | [One sentence] | None/Consumer/Producer |

## Context Relationships

| Upstream (Provider) | Downstream (Consumer) | What's Exchanged |
|--------------------|----------------------|------------------|
| [Context A] | [Context B] | [Data/events] |

## Interface Definitions

### [Context Name]

**NEEDS from other contexts:**
| From Context | What's Needed | Why |
|--------------|---------------|-----|
| [Context] | [Data/capability] | [Purpose] |

**EXPOSES to other contexts:**
| To Context | What's Exposed | Format |
|------------|----------------|--------|
| [Context] | [Data/capability] | [Event/Query] |
```

---

## EXAMPLE: Productivity Coaching App Context Map

```markdown
## Subdomains

### Subdomain: AI Coaching
**Events:** GreetingGenerated, ResponseGenerated, IntentExtracted, GuardrailTriggered
**Classification:** Core
**Rationale:** This IS the product. The coaching experience powered by AI is why users choose this app.

### Subdomain: User Context
**Events:** EnergyAuditRecorded, IntentionSet, SessionOutcomeRecorded
**Classification:** Supporting
**Rationale:** Essential for personalization, but data storage isn't differentiating.

### Subdomain: User Identity
**Events:** AppOpened, UserRegistered
**Classification:** Generic
**Rationale:** Solved problem. Use existing auth solutions.

### Subdomain: Notifications
**Events:** ReminderScheduled, ReminderTriggered
**Classification:** Generic
**Rationale:** Solved problem. Use existing notification infrastructure.

---

## Bounded Contexts

| Context Name | Type | Purpose | AI Involvement |
|--------------|------|---------|----------------|
| AI Coaching Engine | Core | Generates coaching responses, extracts intents | Producer |
| User Context Store | Supporting | Records user history for personalization | None |
| Safety Monitor | Supporting | Evaluates content, enforces guardrails | Consumer |
| User Identity | Generic | Authentication and profiles | None |
| Notifications | Generic | Reminders and alerts | None |

---

## Interface Definitions

### AI Coaching Engine

**NEEDS from other contexts:**
| From Context | What's Needed | Why |
|--------------|---------------|-----|
| User Identity | User profile (name, preferences) | Personalize greeting |
| User Context Store | Recent energy levels, active intentions | Reference in coaching |

**EXPOSES to other contexts:**
| To Context | What's Exposed | Format |
|------------|----------------|--------|
| User Context Store | Extracted intentions | IntentionExtracted event |
| Safety Monitor | Generated content | Pre-delivery content |

### User Context Store

**NEEDS from other contexts:**
| From Context | What's Needed | Why |
|--------------|---------------|-----|
| AI Coaching Engine | Extracted data | Store for future reference |
| User Identity | User ID | Associate data with user |

**EXPOSES to other contexts:**
| To Context | What's Exposed | Format |
|------------|----------------|--------|
| AI Coaching Engine | User history | Query: GetUserContext |
| Notifications | Scheduled blocks | Query: GetUpcomingBlocks |

---

## Visual Context Map

```
                    ┌─────────────────────┐
                    │   User Identity     │
                    │     (Generic)       │
                    └──────────┬──────────┘
                               │ user profile
           ┌───────────────────┼───────────────────┐
           │                   │                   │
           ▼                   ▼                   ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│  AI Coaching    │◄─│  User Context   │  │  Notifications  │
│    Engine       │  │     Store       │◄─│    (Generic)    │
│    (CORE)       │─►│  (Supporting)   │  │                 │
└────────┬────────┘  └─────────────────┘  └─────────────────┘
         │
         │ content for evaluation
         ▼
┌─────────────────┐
│ Safety Monitor  │
│  (Supporting)   │
└─────────────────┘
```
```

---

## COMPLETION CHECKLIST

Do NOT proceed to Bounded Context Canvases until ALL checked:

- [ ] All events grouped into subdomains
- [ ] Each subdomain named with a BUSINESS term (not technical)
- [ ] Each subdomain classified as Core, Supporting, or Generic
- [ ] Classification rationale documented
- [ ] Bounded context boundaries defined
- [ ] Each context has clear, non-overlapping responsibilities
- [ ] Interface definitions complete (NEEDS and EXPOSES)
- [ ] Context map drawn showing relationships

**If AI-POWERED features:**
- [ ] AI experience classified as Core (not accidentally Generic)
- [ ] AI infrastructure distinguished from AI experience
- [ ] AI data flow documented (inputs and outputs)

- [ ] NO technology decisions made

---

## NEXT STEP

"Context Mapping complete. You have [X] contexts. Now define each one in detail. Load `pm-phase-2c-bounded-context-canvas.md` for your Core context first."
