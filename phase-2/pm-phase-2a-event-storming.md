# Phase 2A: Event Storming

**Map everything that HAPPENS in your product** — the events, commands, actors, and policies.

Load this AFTER completing Phase 1 (PRD, and AI Extension if applicable).

---

## CRITICAL RULES

### PRD MUST BE COMPLETE FIRST

You need the user flows from Phase 1 as input. If incomplete, STOP and go finish it.

### NO TECHNOLOGY DECISIONS

Event Storming is about WHAT HAPPENS in your business domain.

**FORBIDDEN:**
- Database tables
- API endpoints
- Code structure
- Framework choices

If you're thinking about HOW to build something, STOP. Wrong mindset.

### USE PAST TENSE FOR EVENTS

Domain events are things that HAPPENED. They are facts.

**CORRECT:** "IntentionSet", "SessionCompleted", "EnergyAuditRecorded"
**WRONG:** "SetIntention", "CompleteSession", "RecordEnergyAudit"

### USE IMPERATIVE FOR COMMANDS

Commands are actions that CAUSE events. They are requests (that might fail).

**CORRECT:** "SetIntention", "CompleteSession"
**WRONG:** "IntentionSet", "SessionCompleted"

---

## CONCEPTS

### Domain Events
Significant things that happened in your system. Always past tense. Other parts of your system react to them.

**Examples:** "UserRegistered", "OrderPlaced", "PaymentProcessed"

### Commands
Actions that trigger events. Imperative form. Might succeed or fail.

**Relationship:** Command → (if successful) → Event

### Actors
WHO or WHAT issues commands:
- **Users:** Real people
- **System:** Automated processes, timers
- **External Systems:** Third-party services

### Policies
Automatic rules: "When X happens, then do Y."

**Format:** "When [Event], then [Command]"

**Example:** "When OrderPlaced, then SendConfirmationEmail"

### Hot Spots
Unresolved questions, risks, or areas of confusion discovered during Event Storming. Capture them—they often reveal critical product decisions.

---

## PROCESS

### Step 1: List Your User Flows
Pull the user flows from your Phase 1 PRD. Each major flow will be event-stormed separately.

### Step 2: For Each Flow, List Domain Events
Go through and write down everything that HAPPENS (past tense).

### Step 3: Arrange Events in Timeline Order
Put events in chronological order, left to right.

### Step 4: Add Commands
For each event: "What action triggered this event?"

### Step 5: Add Actors
For each command: "Who or what issues this command?"

### Step 6: Add Policies
Look for automatic rules: "When this event happens, does anything automatically happen next?"

### Step 7: Mark Hot Spots
Any time you're uncertain—mark it. Don't ignore these.

### Step 8: Review and Refine
Walk through the entire flow. Ask: "What could go wrong here?"

---

## [AI-POWERED] ADDITIONAL CONSIDERATIONS

If your product has AI-GENERATIVE features, add these to your event storming:

### AI-Specific Event Types

**Generation Events** — AI produces output:
- "ResponseGenerated"
- "ContentCreated"
- "SuggestionGenerated"

**Extraction Events** — AI derives structured data:
- "IntentExtracted"
- "SentimentDetected"
- "EntityRecognized"

**Evaluation Events** — AI output is checked:
- "SafetyCheckPassed"
- "QualityThresholdMet"
- "GuardrailTriggered"

**Fallback Events** — AI fails or is uncertain:
- "ConfidenceBelowThreshold"
- "FallbackActivated"
- "ServiceUnavailable"

### Label Your Events

Mark each event as:
- `[DETERMINISTIC]` — Traditional, predictable behavior
- `[AI-POWERED]` — Generative, may vary

**Example:**
```
1. User → OpenApp → AppOpened [DETERMINISTIC]
2. System → GenerateGreeting → GreetingGenerated [AI-POWERED]
3. User → ProvideInput → UserInputReceived [DETERMINISTIC]
4. AI → ExtractIntent → IntentExtracted [AI-POWERED]
```

### AI Commands Have Multiple Outcomes

Unlike deterministic commands, AI commands might:
- Succeed with high confidence
- Succeed with low confidence
- Fail entirely
- Trigger a guardrail

Document these possibilities:

```
Command: ExtractIntent
Possible Events:
  - IntentExtracted (confidence > 0.7)
  - IntentUncertain (confidence < 0.7)
  - ExtractionFailed (error)
```

### Fallback Paths

For every AI command, document what happens when it fails:

```
Fallback: Cannot Extract Intent
- Trigger: AI confidence below threshold after 2 attempts
- Events: FallbackPromptGenerated → SimpleUIDisplayed
- Recovery: User provides structured input instead
```

### Guardrail Triggers

Document what happens when AI hits constraints:

```
Guardrail: Prohibited Topic Detected
- Trigger: User asks for medical advice
- Events: GuardrailTriggered → BoundaryResponseGenerated
- User Experience: Polite decline, redirect to appropriate resources
```

---

## EVENT STORM TEMPLATE

Complete one for EACH major user flow.

```markdown
## Event Storm: [Flow Name]

### Source
User Flow from PRD: [Which flow this maps to]

### Timeline

**1. [Actor]**
- **Command:** [Action in imperative form]
- **Event:** [Result in past tense] [DETERMINISTIC/AI-POWERED]
- **Policy:** [If any: "When X, then Y"]

**2. [Actor]**
- **Command:** [Action]
- **Event:** [Result] [DETERMINISTIC/AI-POWERED]
- **Policy:** [If any]

[Continue for entire flow...]

### [AI-POWERED] Fallback Paths (if applicable)

**Fallback 1: [Scenario]**
- **Trigger:** [What causes fallback]
- **Events:** [What happens]
- **Recovery:** [How to get back to happy path]

### [AI-POWERED] Guardrail Triggers (if applicable)

**Guardrail 1: [Name]**
- **Trigger:** [What activates]
- **Events:** [What happens]
- **User Experience:** [What user sees]

### Hot Spots
- [Question or uncertainty]
- [Risk identified]
- [Decision needed]

### Events Summary

**[DETERMINISTIC] Events:**
- [Event 1]
- [Event 2]

**[AI-POWERED] Events:**
- [Event 1]
- [Event 2]
```

---

## EXAMPLE: Morning Check-In Flow (Productivity Coaching App)

```markdown
## Event Storm: Morning Check-In

### Source
User Flow from PRD: "Flow 1: Morning Intention Setting"

### Timeline

**1. User**
- **Command:** OpenApp
- **Event:** AppOpened [DETERMINISTIC]
- **Policy:** When AppOpened AND morning AND no check-in today → InitiateCheckIn

**2. System (via Policy)**
- **Command:** InitiateCheckIn
- **Event:** CheckInStarted [DETERMINISTIC]

**3. AI System**
- **Command:** GenerateGreeting
- **Event:** GreetingGenerated [AI-POWERED]
- **Possible Outcomes:**
  - Personalized greeting using context
  - Generic greeting if context unavailable

**4. User**
- **Command:** ProvideInput
- **Event:** UserInputReceived [DETERMINISTIC]
- **Data:** {rawText: "I'm feeling about a 6 today, bit tired"}

**5. AI System**
- **Command:** ExtractEnergyLevel
- **Event:** EnergyLevelExtracted OR ExtractionUncertain [AI-POWERED]
- **Policy:** When ExtractionUncertain → RequestClarification

**6. System**
- **Command:** RecordEnergyAudit
- **Event:** EnergyAuditRecorded [DETERMINISTIC]

**7. AI System**
- **Command:** GenerateIntentionPrompt
- **Event:** IntentionPromptGenerated [AI-POWERED]

**8. User**
- **Command:** SetIntention
- **Event:** IntentionSet [DETERMINISTIC]
- **Policy:** When IntentionSet → OfferFocusScheduling

### [AI-POWERED] Fallback Paths

**Fallback 1: Cannot Extract Energy Level**
- **Trigger:** AI confidence < 0.5 after 2 attempts
- **Events:** FallbackPromptGenerated → SimpleScaleDisplayed
- **Recovery:** User clicks 1-10 scale, proceeds normally

**Fallback 2: User Goes Off-Topic**
- **Trigger:** Input unrelated to check-in
- **Events:** OffTopicDetected → GentleRedirectGenerated
- **Recovery:** AI acknowledges, redirects to energy/intention

### [AI-POWERED] Guardrail Triggers

**Guardrail 1: Crisis Detection**
- **Trigger:** User may be in distress
- **Events:** CrisisIndicatorDetected → SupportResourcesProvided
- **User Experience:** Empathetic response, links to help, option to continue

### Hot Spots
- What's the confidence threshold for energy extraction?
- How many clarification attempts before fallback?
- What if user's stated energy contradicts detected sentiment?

### Events Summary

**[DETERMINISTIC] Events:**
- AppOpened
- CheckInStarted
- UserInputReceived
- EnergyAuditRecorded
- IntentionSet

**[AI-POWERED] Events:**
- GreetingGenerated
- EnergyLevelExtracted / ExtractionUncertain
- IntentionPromptGenerated
- (Fallback) FallbackPromptGenerated
- (Fallback) GentleRedirectGenerated
- (Guardrail) SupportResourcesProvided
```

---

## CONSOLIDATING EVENTS

After event-storming all flows, create a master list:

```markdown
## All Domain Events

### [DETERMINISTIC] Events

**User Lifecycle**
- AppOpened
- UserRegistered
- UserProfileUpdated

**Data Recording**
- EnergyAuditRecorded
- IntentionSet
- SessionOutcomeRecorded

### [AI-POWERED] Events

**Generation Events**
- GreetingGenerated
- PromptGenerated
- ResponseGenerated

**Extraction Events**
- IntentExtracted
- EnergyLevelExtracted

**Fallback Events**
- FallbackActivated
- ConfidenceBelowThreshold

**Guardrail Events**
- GuardrailTriggered
- BoundaryResponseGenerated
```

---

## COMPLETION CHECKLIST

Do NOT proceed to Context Mapping until ALL items checked:

- [ ] Every user flow from PRD has been event-stormed
- [ ] All events are named in past tense
- [ ] All commands are named in imperative form
- [ ] Every event has a triggering command
- [ ] Every command has an actor
- [ ] Policies identified ("When X, then Y")
- [ ] Hot spots captured

**If AI-POWERED features:**
- [ ] Events labeled [DETERMINISTIC] or [AI-POWERED]
- [ ] Fallback paths documented for AI failures
- [ ] Guardrail triggers documented
- [ ] AI commands show possible outcomes

- [ ] Master list of all unique events compiled
- [ ] NO technology decisions made

---

## NEXT STEP

"Event Storming complete. Now identify bounded contexts. Load `pm-phase-2b-context-mapping.md`."
