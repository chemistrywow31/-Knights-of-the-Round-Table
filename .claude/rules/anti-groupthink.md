---
name: Anti Groupthink
description: Enforce independent position formation in Roundtable Phase 2 to prevent premature consensus
---

# Anti Groupthink

## Applicability

- Applies to: All roundtable participants (all 14 members when selected for a roundtable, plus life-steward as facilitator)
- Enforcement window: **Roundtable Phase 2 (independent position generation) only**
- Daily mode is explicitly excluded from this rule

## Rule Content

### Independence Mandate

In Roundtable Phase 2, every selected member generates their position without access to any other member's position. Life Steward enforces this by dispatching all Phase 2 tasks in parallel — simultaneous Task calls, one per selected member. No member receives another member's position before submitting their own.

Sequential collection with "ignore other members' positions" instructions is prohibited. Instructional enforcement is weaker than structural enforcement. Parallel dispatch is the required structural mechanism.

### Position Format Requirement

Every Phase 2 position must include all five components:

1. **Stance**: The member's clear position on the decision
2. **Reasoning**: Why this position is correct, with evidence
3. **Confidence level**: Numeric score from 1 (low) to 5 (high)
4. **Key risks identified**: What could go wrong with this approach
5. **Falsification condition**: What evidence would change this position

Positions missing the confidence level are rejected by Life Steward and must be resubmitted.

### No Filtering Before Reveal

In Phase 3 (position reveal), Life Steward presents ALL member positions to the user simultaneously. Life Steward must not:
- Summarize positions before presenting them
- Filter out minority positions
- Order positions by agreement with each other
- Editorialize or contextualize positions before the user reads them

The user sees the raw positions first. Life Steward's synthesis comes in Phase 5, not Phase 3.

### Disagreement Is an Expectation

Every member's agent.md must include a Disagreement Protocol section. Disagreement with other members is an expectation, not a permission. Members must not soften disagreements to maintain harmony.

When members disagree, they must state: "I disagree with {member} because {specific reason}. The correct approach is {alternative} because {evidence}."

### Devil's Advocate Activation

If all Phase 2 positions align (confidence-weighted spread of less than 1 point across all positions), Life Steward must explicitly activate the most relevant contrarian voice and request: "Provide the strongest opposing case you can build."

Devil's advocate activation is mandatory when positions cluster. It is not optional.

### Impasse Protocol

Consensus is not required. If members cannot reach agreement after Phase 4 deliberation, Life Steward presents the disagreement map to the user:
- Member X holds position A at confidence level N
- Member Y holds position B at confidence level N
- The fundamental disagreement is: {what the members disagree about at root}

The user decides. Forced agreement — a member abandoning their position without new evidence — is a violation.

## Violation Determination

- Phase 2 positions dispatched sequentially instead of in parallel → Violation
- Member submits a Phase 2 position without a numeric confidence level → Violation
- Life Steward filters, reorders, or editorializes positions before presenting them to the user → Violation
- All positions align and Life Steward does not activate devil's advocate → Violation
- A member changes their position in response to social pressure without citing new evidence → Violation
- Life Steward forces a synthesis conclusion when members are in genuine impasse → Violation

## Exceptions

- In Phase 4 deliberation (after positions are revealed), members may update their positions in response to other members' arguments. This is legitimate persuasion, not groupthink, provided the position update cites the specific argument that changed their reasoning.
