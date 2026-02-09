# Phase 2C: Bounded Context Canvas

**Create a detailed specification for ONE bounded context.**

**INVOKE THIS ONCE FOR EACH BOUNDED CONTEXT.** Do Core contexts first.

Load this AFTER completing Context Mapping (Phase 2B).

---

## CRITICAL RULES

### CONTEXT MAPPING MUST BE COMPLETE FIRST

Do NOT fill out a canvas until:
- All subdomains identified
- All bounded contexts defined
- Context map with relationships exists
- Interface definitions (NEEDS/EXPOSES) drafted

### ONE CONTEXT AT A TIME

Complete the canvas for ONE context fully before starting another. This prevents confused boundaries and overlapping responsibilities.

### NO TECHNOLOGY DECISIONS

The canvas describes WHAT this context does, not HOW it's built.

**FORBIDDEN:**
- Database tables
- API endpoints
- Code structure
- Framework choices

### INTERFACES ARE CONTRACTS

What this context EXPOSES becomes a promise. Other contexts will depend on it. Document it precisely.

### BUSINESS RULES MUST BE EXPLICIT

Every constraint, validation, and invariant must be documented. If a rule exists in your head but not on the canvas, it will be implemented inconsistently.

---

## CONCEPTS

### Entities
Things with identity that persist through changes. A User is the same user even if they change their name.

**In this context:** List key entities THIS context owns. Only entities whose source of truth is THIS context.

### Value Objects
Things defined by their attributes, not identity. Two $20 bills are equal and interchangeable.

**In this context:** List value objects used in this context.

### Aggregates
A cluster of entities and value objects treated as one unit. Has a "root" entity—the only thing external code can reference.

**Example:** An Order (root) contains LineItems, ShippingAddress, Payment. You can't change a line item without going through the Order.

### Business Rules
Constraints that must ALWAYS be true. Invariants the system must enforce.

**Examples:**
- "Cannot add messages to a completed session"
- "Energy level must be between 1 and 10"

---

## CANVAS TEMPLATE

```markdown
# Bounded Context Canvas: [Context Name]

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | [Context name] |
| **Type** | Core / Supporting / Generic |
| **AI Involvement** | None / Consumer / Producer / Both |
| **Owner** | [Who is responsible] |

**Purpose Statement:**
[2-3 sentences describing what this context does and why it exists. BUSINESS language, not technical.]

---

## Ubiquitous Language (This Context Only)

| Term | Meaning in THIS Context |
|------|-------------------------|
| [Term] | [Definition] |

---

## Responsibilities

**What this context OWNS:**
- [Responsibility 1]
- [Responsibility 2]

**What this context does NOT own:**
- [Explicitly list what belongs elsewhere]

---

## Key Entities

| Entity | Description | Key Attributes | Identifier |
|--------|-------------|----------------|------------|
| [Name] | [What it represents] | [Main attributes] | [Unique ID] |

---

## Value Objects

| Value Object | Description | Attributes |
|--------------|-------------|------------|
| [Name] | [What it represents] | [Components] |

---

## Aggregates

| Aggregate Root | Contains | Key Invariants |
|----------------|----------|----------------|
| [Root entity] | [What's inside] | [Rules that must always be true] |

---

## Domain Events Published

| Event Name | Trigger | Data Included | Consumers |
|------------|---------|---------------|-----------|
| [EventName] | [What causes this] | [Fields] | [Which contexts] |

---

## Commands Accepted

| Command | Actor | Preconditions | Effect | Resulting Event |
|---------|-------|---------------|--------|-----------------|
| [Command] | [Who can issue] | [What must be true] | [What changes] | [Event emitted] |

---

## Queries Answered

| Query | Input | Output | Used By |
|-------|-------|--------|---------|
| [QueryName] | [Parameters] | [What's returned] | [Which contexts] |

---

## Interfaces

### NEEDS from Other Contexts

| From Context | What's Needed | Format | Why Needed |
|--------------|---------------|--------|------------|
| [Context] | [Data/capability] | [Event/Query] | [Purpose] |

### EXPOSES to Other Contexts

| To Context | What's Exposed | Format | Contract |
|------------|----------------|--------|----------|
| [Context] | [Data/capability] | [Event/Query] | [Guarantees] |

---

## Business Rules

1. **[Rule name]:** [Explanation]
2. **[Rule name]:** [Explanation]

---

## Policies

| Trigger Event | Action | Conditions |
|---------------|--------|------------|
| [Event] | [What happens automatically] | [Any conditions] |

---

## Open Questions

- [Unresolved question]
- [Decision needed]
```

---

## [AI-POWERED] ADDITIONAL SECTIONS

If `AI Involvement != None`, add these sections to your canvas:

```markdown
## AI Behavior Properties

Properties that AI outputs from this context MUST exhibit.

### Response Properties

| Property | Specification | How to Measure |
|----------|---------------|----------------|
| **Length** | [e.g., 2-4 sentences] | Word/sentence count |
| **Tone** | [e.g., Encouraging, professional] | Human evaluation rubric |
| **Structure** | [e.g., Question followed by suggestion] | Pattern matching |

### Behavioral Properties

| Property | Specification | How to Measure |
|----------|---------------|----------------|
| **Actionability** | [e.g., Includes next step 80%+ of time] | Human evaluation |
| **Relevance** | [e.g., On-topic 95%+] | LLM-as-judge |
| **Consistency** | [e.g., Persona maintained across turns] | Human evaluation |

---

## Guardrails

Hard constraints. The AI must NEVER violate these.

### Prohibited Behaviors

| Guardrail | Description | Detection Method | Response When Triggered |
|-----------|-------------|------------------|------------------------|
| [Name] | [What's prohibited] | [How detected] | [What happens instead] |

### Required Behaviors

| Guardrail | Description | Enforcement |
|-----------|-------------|-------------|
| [Name] | [What's required] | [How enforced] |

---

## Evaluation Criteria

### Automated Metrics

| Metric | Tool/Method | Target | Frequency |
|--------|-------------|--------|-----------|
| [Metric] | [How measured] | [Target value] | [How often] |

### Human Evaluation

| Evaluation Type | Who | What They Assess | Frequency |
|-----------------|-----|------------------|-----------|
| [Type] | [Evaluator] | [Criteria] | [How often] |

---

## Fallback Behaviors

| Scenario | Detection | Fallback Response | Recovery Path |
|----------|-----------|-------------------|---------------|
| [Failure type] | [How detected] | [What happens] | [How to recover] |

---

## Example Variations

Show the RANGE of acceptable AI outputs. These demonstrate variation, not "correct answers."

### Example 1: [Scenario]

**Context:** [User situation]

**Acceptable Response A:**
```
[One valid response]
```

**Acceptable Response B:**
```
[Different but equally valid response]
```

**Properties demonstrated:** [Which properties]

**Unacceptable variation:**
```
[What would NOT be okay]
```
Why: [Explanation]
```

---

## EXAMPLE: AI Coaching Engine Canvas

```markdown
# Bounded Context Canvas: AI Coaching Engine

## Overview

| Attribute | Value |
|-----------|-------|
| **Name** | AI Coaching Engine |
| **Type** | Core |
| **AI Involvement** | Producer |
| **Owner** | Product team |

**Purpose Statement:**
Delivers AI-guided productivity coaching through natural conversation. Generates contextual prompts, extracts user intentions and energy levels, and applies productivity frameworks to help users be more productive. This is the product's core value — the coaching experience that differentiates it.

---

## Ubiquitous Language (This Context Only)

| Term | Meaning in THIS Context |
|------|-------------------------|
| Response | AI-generated message to the user |
| Extraction | Deriving structured data from user's natural language |
| Prompt | AI-generated question or suggestion to guide user |
| Coaching Flow | A structured conversation pattern (e.g., "morning check-in") |
| Turn | One exchange: user input + AI response |

---

## Responsibilities

**What this context OWNS:**
- Generating coaching responses based on user input and context
- Extracting structured data (intentions, energy levels) from natural language
- Maintaining coaching persona and tone consistency
- Applying appropriate productivity techniques at the right moment
- Managing conversation coherence within a session

**What this context does NOT own:**
- Storing user history long-term (User Context Store)
- Authenticating users (User Identity)
- Evaluating content safety (Safety Monitor)
- Sending notifications (Notifications)

---

## Key Entities

| Entity | Description | Key Attributes | Identifier |
|--------|-------------|----------------|------------|
| CoachingSession | Active conversation with user | userId, state, currentFlow, turnCount | sessionId (UUID) |
| ConversationTurn | One user input + AI response pair | userInput, aiResponse, extractedData, timestamp | turnId (UUID) |

---

## Value Objects

| Value Object | Description | Attributes |
|--------------|-------------|------------|
| UserContext | Snapshot of user data for AI | recentEnergy[], activeIntentions[], preferences |
| ExtractedIntention | Structured intention from natural language | text, type, urgency, confidence |
| ExtractedEnergy | Structured energy level | level (1-10), confidence, emotionalContext |

---

## Aggregates

| Aggregate Root | Contains | Key Invariants |
|----------------|----------|----------------|
| CoachingSession | ConversationTurns (ordered list), CurrentFlow, SessionState | Turns must be chronological. Cannot add turns to completed session. |

---

## Domain Events Published

| Event Name | Trigger | Data Included | Consumers |
|------------|---------|---------------|-----------|
| ResponseGenerated | AI produces response | sessionId, responseText | Safety Monitor |
| IntentionExtracted | AI extracts intention | sessionId, intentionText, confidence | User Context Store |
| EnergyLevelExtracted | AI extracts energy | sessionId, level, confidence | User Context Store |
| FallbackActivated | AI couldn't process | sessionId, reason | Monitoring |

---

## Commands Accepted

| Command | Actor | Preconditions | Effect | Resulting Event |
|---------|-------|---------------|--------|-----------------|
| GenerateResponse | Orchestrator | Active session exists | AI produces response | ResponseGenerated |
| ExtractIntention | Internal | User input received | Structured intention created | IntentionExtracted |
| StartCoachingFlow | Orchestrator | Session active | AI enters specific flow | CoachingFlowStarted |

---

## Interfaces

### NEEDS from Other Contexts

| From Context | What's Needed | Format | Why Needed |
|--------------|---------------|--------|------------|
| User Identity | User profile (name, preferences) | Query | Personalize greeting |
| User Context Store | Recent energy levels (7 days) | Query | Reference in coaching |
| User Context Store | Active intentions | Query | Know what user is working on |

### EXPOSES to Other Contexts

| To Context | What's Exposed | Format | Contract |
|------------|----------------|--------|----------|
| User Context Store | Extracted intentions | Event | Contains: text, type, urgency, confidence (>0.7) |
| Safety Monitor | Generated content | Pre-delivery | Raw response for evaluation |

---

## Business Rules

1. **One active session per user:** Cannot have multiple active sessions.
2. **Extraction confidence threshold:** Only publish events when confidence > 0.7.
3. **Turn limit:** Sessions should not exceed 20 turns.
4. **Persona consistency:** All responses must maintain coach persona.

---

## AI Behavior Properties

### Response Properties

| Property | Specification | How to Measure |
|----------|---------------|----------------|
| **Length** | 2-4 sentences per response | Sentence count |
| **Tone** | Encouraging but not patronizing | Human rubric 1-5 |
| **Structure** | Acknowledgment → Insight → Suggested action | Pattern analysis |

### Behavioral Properties

| Property | Specification | How to Measure |
|----------|---------------|----------------|
| **Actionability** | 80%+ include concrete next step | Human evaluation |
| **Relevance** | 95%+ on-topic | LLM-as-judge |

---

## Guardrails

### Prohibited Behaviors

| Guardrail | Description | Detection | Response |
|-----------|-------------|-----------|----------|
| No Medical Advice | Never diagnose or recommend treatment | Keyword + intent | Acknowledge, suggest professional help |
| No False Promises | Never guarantee outcomes | Pattern matching | Use encouraging but honest language |

### Required Behaviors

| Guardrail | Description | Enforcement |
|-----------|-------------|-------------|
| AI Disclosure | Disclose AI nature if asked | Response rule |
| Uncertainty | Acknowledge when unsure | Confidence threshold |

---

## Fallback Behaviors

| Scenario | Detection | Fallback | Recovery |
|----------|-----------|----------|----------|
| Cannot understand | Confidence <0.5 | Ask clarifying question | User clarifies |
| Off-topic | Topic classification | Gentle redirect | Guide back to coaching |
| Service unavailable | API timeout | Static options | Queue for retry |

---

## Example Variations

### Example 1: Morning Greeting

**Context:** User "Marcus" opens app at 8:15am, energy was 6 yesterday

**Acceptable Response A:**
```
Good morning, Marcus! How are you feeling today? I see you're working on the Q1 roadmap—want to make that your focus?
```

**Acceptable Response B:**
```
Hey Marcus! Before we dive in, quick energy check—how are you feeling this morning, 1 to 10?
```

**Properties demonstrated:** Personalization ✓, Tone ✓, Length ✓

**Unacceptable:**
```
Hello. What do you want to do today?
```
Why: Too cold, no personalization, not encouraging
```

---

## COMPLETION CHECKLIST

Before considering this canvas DONE:

**Standard Sections:**
- [ ] Purpose statement clear and in business language
- [ ] Ubiquitous language terms defined
- [ ] Responsibilities explicit and non-overlapping
- [ ] All entities have identifiers
- [ ] All aggregates have invariants
- [ ] All domain events include data fields
- [ ] All commands include preconditions
- [ ] NEEDS/EXPOSES specific with contracts
- [ ] Business rules explicit
- [ ] Policies defined with triggers

**AI-Specific Sections (if AI Involvement != None):**
- [ ] AI Behavior Properties with measurement methods
- [ ] Guardrails (prohibited AND required)
- [ ] Evaluation criteria (automated + human)
- [ ] Fallback behaviors for all failure scenarios
- [ ] 2-3 Example Variations showing acceptable range
- [ ] Examples show what's UNacceptable and why

---

## AFTER COMPLETING ALL CANVASES

1. Review all canvases together
2. Check for overlapping responsibilities (should be none)
3. Verify interfaces match (what A exposes = what B needs)
4. Confirm no context references data it doesn't have access to
5. **For AI contexts:** Verify guardrails are consistent across contexts

---

## NEXT STEP

"All canvases complete. Phase 2 done! Now make technology decisions. Load `pm-phase-3-technical-architecture.md`."
