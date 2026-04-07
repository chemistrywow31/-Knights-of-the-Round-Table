---
name: Life Review
description: Structured periodic assessment across all life domains using a member-mapped Wheel of Life with optional Ikigai overlay
---

# Life Review

## Description

Life Review is a structured session-length assessment of the user's life across all active domains. Each domain member assesses their dimension (current state, trajectory, wins, concerns). The thinking core synthesizes cross-domain patterns and leverage points. Perspective amplifiers provide reframing if domain reviews surface existential or directional questions. The output is a consolidated review document the user can act on.

## Users

This skill is used by the following agents:
- `butler`: Drives agenda, routes to each member, synthesizes cross-domain output
- Domain Core members: Each reviews their primary dimension
- Domain Partners members: Each reviews their dimension
- `strategist`, `systems-thinker`: Cross-domain synthesis
- `philosopher`, `historian`, `tech-futurist`: Perspective amplification (when triggered)
- `socrates`: Does NOT participate by default (dialectic questioning is not a domain review activity)

## Core Knowledge

### Domain-to-Member Mapping

Each review dimension is owned by exactly one member:

| Dimension | Owner | Review Focus |
|-----------|-------|--------------|
| Career & Business | business-strategist | Current trajectory, leadership, professional growth |
| Entrepreneurship | startup-partner | Venture status, founder psychology, milestones |
| Creative Work | creative-mentor | Active projects, creative health, voice development |
| Financial Health | cfo | Net worth trajectory, risk exposure, plan adherence |
| Emotional Wellbeing | psychologist | Psychological health, patterns, support systems |
| Physical Health | health-advisor | Energy, sleep, fitness, lifestyle sustainability |
| Relationships | relationship-coach | Key relationship health, communication patterns |
| Legal & Risk | legal-counsel | Exposure, open items, risk mitigation status |

**Perspective Amplifiers** (activate only when triggered — see below):
- philosopher: Meaning and purpose questions
- historian: Historical pattern recognition
- tech-futurist: Technology trajectory impact

### Domain Assessment Structure

Each member produces a domain assessment using this template:

```
## {Dimension} Review — {member-name} — {date}

**Current State** (evidence-based, not impressionistic):
{2-4 sentences describing where things actually are, grounded in profile and memory}

**Trajectory**: Improving | Stable | Declining | Unclear
**Trajectory evidence**: {1-2 specific data points from profile or recent sessions}

**Key Wins Since Last Review**:
- {Win 1 — specific, not generic}
- {Win 2}

**Concerns**:
- {Concern 1 — specific, with evidence}
- {Concern 2}

**Recommended Focus for Next Period**:
{One concrete recommendation with rationale — not a list of everything the member thinks}

**Score**: {1-10, where 1=critical dysfunction, 10=thriving}
**Score Rationale**: {1 sentence justifying the score}
```

Scores must be evidence-based. A member cannot score a dimension 8/10 if they also identify 2 active concerns without justifying why those concerns don't lower the score.

### Cross-Domain Synthesis (Thinking Core)

After all domain assessments are complete, strategist and systems-thinker produce a joint synthesis:

**Strategist** identifies:
- Which domain's improvement would create the most positive cascade across other domains (highest leverage point)
- Where resources are being allocated suboptimally across domains
- The single most important strategic move for the next 90 days

**Systems-Thinker** identifies:
- Feedback loops between domains (e.g., financial stress → emotional wellbeing decline → reduced creative output)
- Unintended consequences of domain improvements (e.g., pursuing career growth at the cost of relationship health)
- Structural tensions between domains that no single intervention resolves

### Perspective Amplifier Activation

Activate perspective amplifiers when domain reviews surface:

| Trigger | Activate |
|---------|---------|
| Score drop of 3+ points from last review in any dimension | philosopher (meaning questions often accompany sharp declines) |
| User expresses loss of direction or purpose | philosopher |
| Multiple domains declining simultaneously | historian (historical parallels for navigating convergent pressures) |
| Technology or industry disruption concern | tech-futurist |
| User asks "Is this worth it?" or "Am I on the right path?" | philosopher + (optionally) historian |

Do NOT activate perspective amplifiers for: normal score fluctuations, tactical concerns, or operational questions.

### Ikigai Overlay (Optional)

Activate Ikigai overlay when:
- User requests it explicitly
- Last review Ikigai overlay was more than 6 months ago
- Domain reviews reveal a persistent sense of misalignment or purpose questions

The Ikigai overlay evaluates alignment across four dimensions:

| Ikigai Question | Team Members Who Address It |
|-----------------|----------------------------|
| What do you love? | creative-mentor, philosopher |
| What are you good at? | business-strategist, strategist |
| What does the world need? | startup-partner, philosopher |
| What can you be paid for? | cfo, business-strategist |

Ikigai output: One paragraph on current alignment, one on identified gaps, one on one concrete next step.

### Output Document Structure

The consolidated review is presented to the user as:

```
# Life Review — {date}

## Domain Scores Overview
| Domain | Score | Trajectory | Responsible Partner |
...{table}...

## Detailed Domain Assessments
{Each member's assessment, in full}

## Cross-Domain Synthesis
{strategist's leverage point analysis}
{systems-thinker's loop and tension analysis}

## Perspective Extension (if applicable)
{philosopher / historian / tech-futurist input, if activated}

## Ikigai Overlay (if applicable)
{Ikigai overlay, if requested}

## Recommended Priority Actions (Next 90 Days)
{Top 3 recommendations, ranked by impact x feasibility}
```

## Application Guide

### Scenario A: Scheduled Review (User Requests)

1. Coordinator confirms review intent and estimated time: "This comprehensive review will take approximately a full conversation session. Do you have the time now?"
2. Coordinator reads profile and memory to identify which domains need depth
3. Dispatch domain members for assessments (parallel where possible, then sequential for cross-domain members)
4. Dispatch strategist and systems-thinker for cross-domain synthesis
5. Check perspective amplifier triggers
6. Optionally offer Ikigai overlay
7. Present consolidated output
8. User responds, discusses, revises priorities
9. Coordinator writes review date to accumulated memory; updates profile objectives

### Scenario B: Unscheduled Review (Pattern-Triggered)

Opening scan detects 3+ domains showing stress signals.

Coordinator proposes: "I have a suggestion — doing a periodic review today might be more valuable than discussing individual issues, because I'm seeing signals across several dimensions at once. Would you like to try it?"

If user agrees: run full life-review skill.
If user declines: run Daily Mode for the most urgent individual domain.

### Rejection/Failure Case: Member Cannot Assess — Incomplete Profile

A domain member's profile section is empty (interview not completed).

**Member response in review**:
> "My data for this domain is still incomplete — we haven't done a full financial interview yet. Based on the limited information you've mentioned in other conversations, my preliminary observation is {limited observation}. But the confidence level for this assessment is low. If you're willing, we can complete the financial interview after this review."

Provide what is possible with clear confidence caveat. Do not refuse to assess entirely. Do not fabricate data.

## Quality Checkpoints

- [ ] All active domain members have provided assessments before synthesis begins
- [ ] Each assessment follows the standard template with all required fields
- [ ] Scores are evidence-based (concerns justify score reductions)
- [ ] Cross-domain synthesis identifies specific leverage points, not generic advice
- [ ] Perspective amplifier activation follows the trigger rules (not activated for routine reviews)
- [ ] Ikigai overlay only runs when explicitly triggered
- [ ] Review date written to accumulated memory after completion
- [ ] Top 3 recommendations are ranked by impact x feasibility, not by member seniority

## Examples

### Normal Case: Quarterly Review, All Dimensions Active

**Setup**: 3-month user, all profile sections complete, last review 6 weeks ago.

**Output excerpt**:
```
| Financial Health | 6/10 | Declining | cfo |
| Entrepreneurship | 7/10 | Stable | startup-partner |
| Career & Business | 8/10 | Improving | business-strategist |
```

Systems-thinker synthesis: "The career growth is real, but it's absorbing the time and energy that was previously devoted to the startup project — this is a classic resource crowding-out loop. If this continues, the entrepreneurship score will start declining within three months."

### Edge Case: Multiple Dimensions Declining — Philosopher Triggered

**Setup**: Score drops of 4+ points in financial health AND emotional wellbeing from last review.

**Philosopher activated**: "Two key dimensions declining sharply at the same time — I want to ask a more fundamental question: under this pressure, has your sense of meaning in what you're doing been shaken? This isn't to negate your choices, but these moments are often when values need to be reaffirmed."

### Rejection/Failure Case: User Wants Scores Only, No Analysis

**User**: "No time today, just give me the scores"

**Coordinator response**:
> "Sure — I can give you a quick version: just scores and a one-sentence summary per domain, no full analysis. About 5 minutes. Would that work for you?"

If user confirms: each member provides score + one sentence only. Skip synthesis. Skip perspective amplifiers. Write abbreviated entry to accumulated memory.

Do not force the full format when the user has limited time.
