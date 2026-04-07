---
name: Roundtable Protocol
description: Multi-member deliberation for major decisions that enforces independent positions before cross-member debate
---

# Roundtable Protocol

## Description

Roundtable Protocol governs how the team handles major decisions. It enforces a non-negotiable sequence: independent positions first, simultaneous reveal, then open deliberation. The independence requirement is structural — positions are generated via parallel dispatch with no cross-visibility. Devil's advocate activation triggers automatically if positions cluster. The user makes the final decision; consensus is not a goal.

## Users

This skill is used by the following agents:
- `butler`: Facilitates all phases, enforces independence, produces synthesis
- All 14 members: Participate in Phase 2 (position generation) and Phase 4 (deliberation) when selected

## Core Knowledge

### When to Activate

Activate roundtable-protocol when ANY of the following is true:
- User explicitly requests: "I want to hear everyone's opinion" / "This decision is important" / "Open a roundtable discussion for me"
- Decision spans 2+ life domains (e.g., career change that affects finances AND family)
- Decision is difficult to reverse (quitting a job, major investment, ending a relationship)
- Decision has long-term consequences (affects 12+ months of life trajectory)

Do NOT activate for: tactical questions, information requests, emotional support conversations, or decisions the user has already clearly made and is not reconsidering.

### Member Selection (3-5 per roundtable)

Select members by domain relevance to the specific decision. Always include:
- At least one thinking-core member (strategist, systems-thinker, or socrates) for analytical rigor
- Domain members whose expertise directly applies
- Maximum 5 total — more creates noise, not insight

Selection statement to user: "I'll bring in [member names] for this discussion, because [one sentence on why each]. Other partners can join in the second round if needed."

### Phase 1 — Question Framing

The coordinator states the decision question precisely. A poorly framed question produces misaligned positions.

Format:
```
Question: {One precise decision question}
Context: {2-3 sentences of relevant context}
Constraints: {Any hard constraints the user has stated}
Out of scope: {What is already decided or off the table}
```

Confirm with user before proceeding: "Does this framing accurately capture the question?"

### Phase 2 — Independent Position Generation

**This phase uses parallel dispatch.** All selected members generate their position simultaneously, with no access to each other's responses.

Each position follows this structure:

```
Stance: {One clear stance}
Reasoning: {2-4 key reasons — evidence-based, not generic}
Key risks: {The 1-2 biggest risks I see}
Confidence level: {1-5, where 1=highly uncertain, 5=confident}
Condition to change stance: {What evidence would change my position}
```

No member sees any other member's position during Phase 2. This is enforced by the parallel dispatch architecture — positions are collected privately, not through group conversation.

**Positions without a confidence level are returned for completion. The coordinator does not synthesize incomplete positions.**

### Phase 3 — Position Reveal

Present ALL positions simultaneously. Do not:
- Reorder positions by agreement level
- Summarize or paraphrase before showing
- Add editorial commentary ("Interestingly, two members agree...")
- Filter any position out

Format for reveal:
```
### All Positions (Simultaneous Reveal)

**{member-name} ({confidence}/5)**
Stance: {verbatim}
Reasoning: {verbatim}
Key risks: {verbatim}
Condition to change stance: {verbatim}
```

After presenting all positions: "This is the first round of today's roundtable. Everyone can now see each other's positions. Let's move into deliberation."

### Phase 4 — Deliberation

Members respond to each other's positions. Rules:
- Members may directly challenge each other's reasoning
- Members may update their stated position if genuinely persuaded — state "I'm updating my position" explicitly
- User participates directly — their questions and reactions are inputs, not interruptions
- The coordinator does not moderate content (only process — keep it on topic)

**Devil's Advocate Activation**: If after the first deliberation round, all positions are within 1 point of each other on confidence (e.g., all between 3-4), the coordinator explicitly activates the most relevant contrarian member:

> "{member-name}, please present the strongest possible case against this decision — not your actual position, but the most compelling opposing argument."

This activation is mandatory, not optional. Premature consensus is more dangerous than continued disagreement.

### Phase 5 — Confidence-Weighted Synthesis

After deliberation reaches a stopping point (see below), the coordinator produces synthesis.

**Synthesis is NOT a vote.** It is a confidence-weighted summary:

1. Identify positions that converge (even partially)
2. Identify persistent disagreements — record them as information, not failures
3. Weight each position by: `confidence level x domain relevance to this decision`
4. State the synthesis: "Based on today's discussion, {synthesis statement}. Important to note: {persistent disagreements}. The final decision is yours."

If the team reaches genuine impasse (members remain strongly opposed after full deliberation), state the impasse map:

> "There is no consensus today — and that itself is important information. {member A} and {member B} disagree on {specific disagreement}. You decide which risk you are willing to take."

**Impasse is information. Forced consensus is a violation.**

### Stopping Criteria

Stop deliberation when ANY of the following:
- No meaningful new argument has emerged in the last round (linguistic check: are members repeating the same points?)
- User explicitly stops: "OK, I think that's enough"
- 3 full deliberation rounds have completed (hard limit — prevent exhaustion)

Do NOT stop because members disagree. Disagreement is not a stopping condition.

## Application Guide

### Scenario A: Clean Roundtable (Clear Decision, 4 Members)

User: "I'm considering quitting my job to go all-in on my startup. I'd like to hear what everyone thinks."

Coordinator:
1. Frames question: "Should you leave {current role} within {time frame} to go full-time on {venture}?"
2. Selects: startup-partner, business-strategist, cfo, systems-thinker
3. Dispatches all four in parallel for positions
4. Presents all four simultaneously (no filtering)
5. Opens deliberation
6. Checks for clustering after Round 1 — if yes, activates devil's advocate
7. After stopping criterion met, produces synthesis

### Edge Case: User Tries to Steer Members Toward a Preferred Answer

**Input**: Before Phase 2, user says "I'm pretty sure I want to quit. Just want validation."

**Coordinator response**:
> "I hear your inclination — after everyone gives their independent analysis, you can tell me whether that inclination was reinforced or challenged. For now, let them each analyze independently."

Do not modify Phase 2 question framing to lead toward the user's preferred outcome. The value of the roundtable is in the independence.

### Rejection/Failure Case: Decision Is Already Made, User Seeks Validation Only

**Input**: "I've already decided, just wanted to let everyone know"

**Coordinator response**:
> "The roundtable discussion is designed for decisions that are genuinely open. If you've already decided, I can route you to the relevant partners to discuss execution strategy instead — that would be more helpful. Are you truly still considering, or are you mainly looking to confirm that your decision is sound?"

If user confirms the decision is made: route to relevant domain members for implementation planning. Do not run roundtable-protocol on a closed decision.

## Quality Checkpoints

- [ ] Phase 2 positions collected in parallel (no sequential revealing)
- [ ] All positions presented verbatim in Phase 3 (no filtering or editorializing)
- [ ] Devil's advocate activated if positions cluster within 1 confidence point
- [ ] Synthesis is confidence-weighted, not majority vote
- [ ] Impasse presented transparently if it exists (not papered over)
- [ ] User retains final decision authority (coordinator never decides)
- [ ] Question framing confirmed with user before Phase 2 begins
