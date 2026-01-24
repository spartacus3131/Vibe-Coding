# Phase 1: AI Extension (For Generative AI Features)

**Add this ONLY if your product has AI-GENERATIVE features** — conversation, content creation, coaching, or any AI where the output is DESIGNED to vary.

Complete the Base PRD first. This extension adds AI-specific sections.

---

## WHEN YOU NEED THIS EXTENSION

### You NEED this if:
- AI has a "persona" or "voice" (coaching bot, writing assistant)
- AI output should vary naturally for the same input
- You need to define "tone" or "personality"
- Success is measured by properties ("helpful," "concise") not correctness

### You DON'T need this if:
- AI aims for a "correct" answer (transcription, classification, OCR)
- AI is invisible infrastructure (embeddings, search ranking)
- You could theoretically write exact expected outputs

**The test:** If three expert humans would give three different but equally valid answers, you need this extension.

---

## CRITICAL MINDSET SHIFT

### PROPERTIES, NOT SPECIFICATIONS

You are defining HOW the AI SHOULD BEHAVE, not WHAT it WILL OUTPUT.

**FORBIDDEN in AI requirements:**
- Scripting exact dialogue or responses
- Specifying precise outputs
- Writing "The AI will say..."
- Deterministic acceptance criteria

**REQUIRED:**
- Behavioral properties ("concise," "encouraging," "evidence-based")
- Measurable qualities ("2-4 sentences," "includes next step 80%+ of time")
- Evaluation rubrics, not pass/fail tests

If you find yourself writing exact AI responses, STOP. You're thinking deterministically about non-deterministic behavior.

### VARIATION IS A FEATURE, NOT A BUG

Ask three expert coaches the same question. Each gives different advice—but all three are helpful, relevant, and valuable. None is "wrong."

That's non-deterministic behavior: same input, different outputs, all valid.

---

## THE 5 C'S OF GENERATIVE AI

Before writing anything, answer these:

| Question | What You're Answering |
|----------|----------------------|
| **CAPABILITY** | What can the AI do that traditional code cannot? |
| **CONTEXT** | What information does the AI need to perform well? |
| **CONSTRAINTS** | What must the AI never do? What are hard boundaries? |
| **COHERENCE** | How do you measure if outputs are high-quality? |
| **CONTINGENCY** | What happens when the AI fails or is uncertain? |

If you cannot answer these clearly, you do NOT understand the AI feature well enough.

---

## AI EXTENSION TEMPLATE

Add these sections to your Base PRD:

```markdown
---

# AI EXTENSION

---

## The 5 C's

| Question | Answer |
|----------|--------|
| **CAPABILITY** | [What can the AI do that traditional code cannot?] |
| **CONTEXT** | [What information does the AI need? User history, preferences, conversation state?] |
| **CONSTRAINTS** | [What must the AI never do? Hard boundaries?] |
| **COHERENCE** | [How do you measure quality? User ratings, coherence scores, completion rates?] |
| **CONTINGENCY** | [What happens on failure? Fallbacks, escalation, graceful degradation?] |

---

## AI Persona Definition

**Role:** [e.g., "Productivity coach," "Research assistant," "Creative partner"]

**Personality traits:**
- [Trait 1: e.g., Encouraging but not patronizing]
- [Trait 2: e.g., Concise and action-oriented]
- [Trait 3: e.g., Evidence-based, not prescriptive]

**Expertise level:** [e.g., "Informed by research, speaks practically not academically"]

**Communication style:**
- [Style 1: e.g., Uses "we" language]
- [Style 2: e.g., Asks one question at a time]
- [Style 3: e.g., Acknowledges before redirecting]

**Boundaries — The AI is NOT:**
- [Boundary 1: e.g., "Not a therapist"]
- [Boundary 2: e.g., "Not a decision-maker for user"]
- [Boundary 3: e.g., "Not a medical professional"]

---

## AI Response Properties

Define measurable qualities, NOT exact outputs.

**Tone:** [Specific descriptor—warm, professional, playful, etc.]

**Length:** 
- Per response: [X-Y sentences or Z-W words]
- Rationale: [Why this length?]

**Structure:**
- [How responses should be organized]
- [e.g., "Acknowledgment → Insight → Question"]

**Personalization:**
- [When to use user's name]
- [How to reference past interactions]
- [When to adapt based on patterns]

**Actionability:**
- [e.g., "Includes concrete next step 80%+ of time"]
- [e.g., "Ends with question 60%+ of time"]

---

## Conversation Design (If Conversational AI)

### Conversation Phases

| Phase | Purpose | Required Information | Success Properties | Fallback |
|-------|---------|---------------------|-------------------|----------|
| [Phase 1] | [What to accomplish] | [Data to extract] | [What makes this successful] | [If fails] |
| [Phase 2] | [What to accomplish] | [Data to extract] | [What makes this successful] | [If fails] |

### Conversation Properties

**Turn-Taking:**
- Average conversation length: [X-Y turns]
- Maximum before timeout/escalation: [Z turns]

**Context Management:**
- Session memory: [What to remember within conversation]
- User profile memory: [What to persist across sessions]

**Adaptability:**
- [How system adjusts to user sophistication]
- [How system personalizes based on history]

---

## Guardrails & Constraints

### Prohibited Behaviors

| Guardrail | Description | Detection Method | Response When Triggered |
|-----------|-------------|------------------|------------------------|
| [Name] | [What's prohibited] | [How detected] | [What happens instead] |

Example:
| No Medical Advice | Never diagnose or recommend treatments | Keyword + intent detection | Acknowledge concern, suggest professional, continue |

### Required Behaviors

| Requirement | Description | Enforcement |
|-------------|-------------|-------------|
| [Name] | [What's required] | [How enforced] |

Example:
| AI Disclosure | Disclose AI nature if asked | Response rule |
| Uncertainty | Acknowledge when unsure | Confidence threshold |

---

## Fallback Behaviors

| Failure Scenario | Detection | System Response | User Experience |
|------------------|-----------|-----------------|-----------------|
| Cannot understand user | Confidence < 0.5 | Ask clarifying question | "Could you tell me more about..." |
| Low confidence response | Threshold check | Hedge + offer alternatives | "I'm not certain, but..." |
| Off-topic request | Topic classifier | Gentle redirect | "That's interesting! For our session..." |
| API unavailable | Timeout/error | Static fallback | Pre-written helpful message |
| Guardrail triggered | Content filter | Safe alternative | Boundary response + redirect |

---

## AI Evaluation Framework

### Automated Metrics

| Metric | Tool/Method | Target | Frequency |
|--------|-------------|--------|-----------|
| Response latency (P95) | [Monitoring tool] | [<X seconds] | Real-time |
| Coherence | [LLM-as-judge] | [>Y score] | Weekly sample |
| On-topic rate | [LLM-as-judge] | [>Z%] | Weekly sample |
| Toxicity | [Perspective API / etc.] | [0%] | Every response |

### Human Evaluation

| Type | Who Evaluates | What They Assess | Frequency |
|------|---------------|------------------|-----------|
| Expert review | [Internal team] | [Helpfulness, persona consistency] | Weekly: 50 conversations |
| User feedback | [End users] | [Thumbs up/down, comments] | Every session |
| Red team | [QA team] | [Break persona, elicit prohibited content] | Monthly |

### AI-Specific Business Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| [e.g., Session helpfulness] | % sessions rated thumbs up | >70% |
| [e.g., AI engagement] | % users who use AI feature weekly | >50% |
| [e.g., Task completion via AI] | % intended actions completed after AI | >40% |

---

## Example Conversations (MANDATORY)

You MUST include 3-5 example conversations showing VARIATION.

### Example 1: [Scenario Name - e.g., "Happy Path"]

**User Context:** [Brief description of user type and situation]

**Conversation:**

User: [First message]

**Acceptable Response A:**
> [One valid response]

**Acceptable Response B:**
> [Different but equally valid response]

**Acceptable Response C:**
> [Another valid variation]

**Properties Demonstrated:**
- [Property 1: e.g., "Brevity - 2-3 sentences"]
- [Property 2: e.g., "Personalization - uses name"]
- [Property 3: e.g., "Actionable - provides next step"]

**Unacceptable Response:**
> [What would NOT be okay]

**Why Unacceptable:** [Explanation]

---

### Example 2: [Scenario Name - e.g., "Ambiguous Input"]

[Same format...]

---

### Example 3: [Scenario Name - e.g., "Guardrail Activation"]

[Same format - show how AI handles prohibited topic gracefully]

---

## Data Extraction (If AI Extracts Structured Data)

If the AI extracts structured data from conversation:

### Extraction: [Name]

**Input:** [Natural language from user]
**Output:** [Structured data extracted]

**Extraction Properties:**
- Confidence threshold: [e.g., >0.7 to accept]
- Validation: [e.g., user confirms before saving]
- Fallback: [e.g., ask clarifying question if low confidence]

**Example Extractions:**

| User Input | Extracted Data | Confidence |
|------------|----------------|------------|
| "I need to finish the Q1 roadmap" | {text: "Finish Q1 roadmap", type: "task", urgency: "high"} | 0.9 |
| "maybe work on that thing" | {confidence: 0.3} → Ask clarification | 0.3 |

---

## AI Glossary Additions

Add to your Base PRD glossary:

| Term | Definition |
|------|------------|
| [AI Behavior Term] | [What it means—e.g., "Concise: 2-4 sentences per response"] |
| [Evaluation Term] | [How measured—e.g., "Coherence: LLM-judge score 1-10"] |
| [Technical Term] | [What it is—e.g., "Context window: conversation history available to AI"] |
```

---

## AI EXTENSION COMPLETION CHECKLIST

Do NOT proceed until ALL items are checked:

**Foundation:**
- [ ] 5 C's answered clearly (Capability, Context, Constraints, Coherence, Contingency)
- [ ] AI persona defined with traits and boundaries
- [ ] Response properties specified (measurable, not vague)

**Guardrails:**
- [ ] Prohibited behaviors listed with detection and response
- [ ] Required behaviors listed with enforcement
- [ ] Fallback behaviors for all failure scenarios

**Evaluation:**
- [ ] Automated metrics with tools and targets
- [ ] Human evaluation process defined
- [ ] AI-specific business metrics identified

**Examples:**
- [ ] 3-5 example conversations showing VARIATION
- [ ] Examples show acceptable range, not "correct answers"
- [ ] Unacceptable responses included with explanations
- [ ] Guardrail activation example included

**If AI extracts structured data:**
- [ ] Extraction targets defined
- [ ] Confidence thresholds set
- [ ] Fallback for low confidence documented

---

## AFTER COMPLETING AI EXTENSION

Your Phase 1 is complete when:
1. Base PRD is done ✓
2. AI Extension is done ✓

→ Proceed to Phase 2: Domain Architecture

In Phase 2, you will:
- Label events as [DETERMINISTIC] or [AI-POWERED]
- Create AI-specific bounded context canvases with behavior properties
- The AI Extension informs your AI context design
