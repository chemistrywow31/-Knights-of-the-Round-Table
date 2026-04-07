---
name: Mode Detection
description: Coordinator classifies each session as daily, roundtable, or review mode based on user input and opening scan signals
benefits-from:
  - "opening-scan"
---

# Mode Detection

## Description

Mode Detection classifies each session into one of three operating modes: Daily (responsive conversation with 1-3 members), Roundtable (multi-member deliberation for major decisions), or Review (structured life assessment across all domains). Mode is determined from user input and the opening scan report. Mode can switch mid-session when conditions change. The coordinator announces mode switches explicitly.

## Users

This skill belongs exclusively to `agents/butler.md`

## Core Knowledge

### Three Operating Modes

| Mode | When | Members Activated | Duration |
|------|------|-------------------|----------|
| Daily | Default — user raises a topic, question, or situation | 1-3 members (topic-matched) | Conversation-length |
| Roundtable | Major decision requiring multiple perspectives | 3-5 members (decision-relevant) | Until stopping criterion met |
| Review | Periodic life assessment | All domain members | Full session (60-90 min equivalent) |

### Daily Mode Triggers

Activate Daily Mode when:
- User states a topic, question, or situation without any deliberation signals
- User asks for advice, analysis, or reflection on a specific issue
- User shares news (personal, professional, creative) and wants to discuss
- No roundtable or review trigger is present
- First session with a new user (even if profile is incomplete)

Daily Mode is the DEFAULT. When in doubt, start Daily and escalate if needed.

**Typical openings**: "I've been thinking about..." / "There's a situation lately..." / "What do you think about X?" / "Help me think through Y"

### Roundtable Mode Triggers

Activate Roundtable Mode when ANY of the following:

**Explicit**: User says any of:
- "I want to hear everyone's opinion"
- "This decision is important, I need a full analysis"
- "What does everyone think?"
- "Open a roundtable for me"

**Decision signals** (coordinator detects):
- Decision spans 2+ life domains
- Decision involves significant irreversibility (career change, major investment, relationship ending)
- Decision affects 12+ months of life trajectory
- Stakes described as "very important" / "big change" / "I'm really torn"

**From opening scan**: Scan report recommends Roundtable AND the user's opening confirms a major decision is active.

Do NOT activate Roundtable for: information questions, emotional support conversations, tactical execution questions, or hypothetical explorations.

### Review Mode Triggers

Activate Review Mode when ANY of the following:

**Explicit**: User requests a life review: "Help me do a comprehensive life assessment" / "I'd like to do a periodic review"

**Time-based** (from opening scan): `memory/accumulated.md` shows last review entry was more than 4 weeks ago AND user confirms they are open to a review when coordinator suggests it.

**Pattern-based** (from opening scan): Scan detects 3+ domain pattern signals simultaneously (e.g., financial stress, relationship tension, creative block — all active at once).

**From scan**: Scan report recommends Review AND coordinator states:
> "I noticed several dimensions showing activity at the same time during the opening scan. Do you have time for a more comprehensive review? It would take about a full conversation session."

Review Mode requires user confirmation before starting. Do not enter Review Mode without explicit user agreement.

### Mode Output Structure

After running opening scan, classify mode and produce internal mode report:

```
## Mode Classification — {date}

**Mode**: Daily | Roundtable | Review
**Confidence**: High | Medium | Low
**Trigger**: {What triggered this mode — user statement or scan finding}
**Primary members to activate**: {member-id list}
**Rationale**: {1-2 sentences}
**Escalation condition**: {What would trigger a mode switch mid-session}
```

### Mid-Session Mode Switching

**Daily → Roundtable**: When a topic reveals unexpected complexity or stakes.

Trigger: User reveals the decision is irreversible, high-stakes, or cross-domain.

Action: Coordinator pauses the Daily conversation:
> "As we've been talking, I realize this decision might be more complex than a one-on-one conversation can handle. Would you like to open a roundtable and have several partners look at this together?"

Wait for user confirmation before switching.

**Daily → Review**: When scan-detected patterns are confirmed by the conversation.

Action: Same as above — announce and confirm before switching.

**Roundtable → Daily**: When user realizes the decision is actually already made.

Action: Close roundtable, route to relevant member for implementation support.

**Review → Daily**: When user wants to dive deep on one dimension only.

Action: Acknowledge the shift, route to the relevant domain member.

## Application Guide

### Scenario A: Clear Daily Mode

**Input**: "Today I want to talk about why my new side project isn't progressing as expected"

**Mode detection**: Daily. No deliberation signals. Topic is startup/creative. Activate: startup-partner (primary), creative-mentor (standby if creative dimensions emerge).

Output: Daily mode, medium confidence, primary: startup-partner.

### Scenario B: Ambiguous — Could Be Daily or Roundtable

**Input**: "I'm considering whether to quit my job. I'm a bit torn."

**Mode detection logic**:
- "quit my job" = career change = high stakes
- "considering whether" = still deciding = open decision
- "a bit torn" = uncertainty signal

But: is the user ready for a full roundtable, or do they want to think out loud first?

**Coordinator action**: Start Daily Mode, activate business-strategist for initial discussion. After 2-3 exchanges, check:
> "This decision looks like a big one. Would you like to have more partners weigh in with their analysis, or continue our conversation first?"

Let the user choose. Do not assume Roundtable.

### Rejection/Failure Case: Review Suggested, User Declines

**Scan report**: Last review was 7 weeks ago. Pattern signals: financial stress + creative block detected.

**Coordinator opening**:
> "I see your last comprehensive review was seven weeks ago, and there are a few dimensions showing activity at the same time lately — if you have the time, doing a periodic review today would be quite valuable. Want to give it a try?"

**User response**: "Not today, I have something else I want to talk about"

**Coordinator action**: Immediately accept. Enter Daily Mode. Do not re-suggest Review in the same session.

> "Sure, tell me what's on your mind."

Never force Review Mode. The user controls the agenda.

## Quality Checkpoints

- [ ] Opening scan runs before mode detection (benefits-from dependency satisfied)
- [ ] Daily is the default — mode detection escalates, never defaults to roundtable or review
- [ ] Review Mode requires explicit user confirmation before entering
- [ ] Mid-session mode switches announced to user before executing
- [ ] Mode output structure produced internally before member activation
- [ ] Ambiguous triggers resolved by asking user, not by assuming
