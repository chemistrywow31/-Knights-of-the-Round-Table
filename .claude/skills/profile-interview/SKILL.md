---
name: Profile Interview
description: Multi-session onboarding where each member conducts domain-specific intake to build the user's complete life profile
---

# Profile Interview

## Description

Profile Interview is the onboarding process that transforms a new user into a known person for the entire advisory team. The coordinator orchestrates a sequence of domain-specific intake conversations across multiple sessions, each member asking questions only within their expertise. Output is written to three profile files that all members read for context. Cold-start mitigation ensures members can operate meaningfully even before all domain interviews are complete.

## Users

This skill is used by the following agents:
- `butler`: Orchestrates the sequence, tracks completion status, handles cold-start mitigation
- All 14 members: Each conducts their own domain-specific intake segment

## Core Knowledge

### Profile File Structure

Three files capture the complete profile:

```
profile/
  base.md      ← Identity, demographics, life context (captured in Session 1)
  values.md    ← Core values, beliefs, philosophy, what the user optimizes for
  domains.md   ← Domain-specific data: career, finances, health, relationships, etc.
```

### Onboarding Sequence

**Session 1 — Base Identity (Mandatory First)**

The coordinator runs this directly before any member interview begins. Captures minimum viable profile for cold-start operation.

Required base.md fields:
- Name, age, location
- Current major life situations (work, family, creative)
- Primary reason for using the team
- 2-3 most pressing concerns right now
- Communication preference (how direct, how much challenge)

After Session 1 base capture, members can begin operating. Full domain interviews happen over subsequent sessions.

**Domain Interview Sequence (Sessions 2+)**

Priority order for domain interviews (highest-impact domains first):

| Priority | Member | Domain Covered |
|----------|--------|---------------|
| 1 | strategist | Life goals, decision-making style, blind spots |
| 2 | psychologist | Emotional patterns, coping mechanisms, triggers |
| 3 | business-strategist | Career trajectory, professional context |
| 4 | startup-partner | Entrepreneurial history, current ventures |
| 5 | creative-mentor | Creative work, aesthetic preferences, blocks |
| 6 | cfo | Financial situation, risk tolerance, goals |
| 7 | health-advisor | Physical health, lifestyle, energy patterns |
| 8 | relationship-coach | Key relationships, communication patterns |
| 9 | philosopher | Values, worldview, existential questions |
| 10 | systems-thinker | How user sees interconnections in their life |
| 11 | socrates | Recurring assumptions the user holds |
| 12 | legal-counsel | Legal situation, risk exposure (if relevant) |
| 13 | historian | How user interprets their own history |
| 14 | tech-futurist | Tech relationship, industry context |

### Domain Interview Questions by Member

**strategist** — Ask about:
- Long-term vision (3, 10, 20 year horizon)
- Resource constraints (time, money, energy, relationships)
- Decisions consistently avoided — why?
- What "winning" looks like for this person

**psychologist** — Ask about:
- Emotional patterns under stress
- Coping mechanisms (healthy and unhealthy)
- Known triggers and reactions
- Recurring relationship dynamics
- Self-perception vs. how others perceive them

**business-strategist** — Ask about:
- Current role and organization
- Career trajectory and next move
- Key professional relationships and competitors
- Leadership challenges and organizational dynamics

**startup-partner** — Ask about:
- Current ventures and their status
- Past startup experiences and lessons
- Founder identity and psychology
- Relationship with failure and uncertainty

**creative-mentor** — Ask about:
- Active creative projects
- Creative influences and aesthetic preferences
- Recurring creative blocks
- How they evaluate quality in their own work

**cfo** — Ask about:
- Income sources and stability
- Savings, investments, debts
- Financial risk tolerance (specific scenarios, not abstract)
- Financial goals and timeline
- Money beliefs and emotional relationship with money

**health-advisor** — Ask about:
- Current fitness and health status
- Sleep quality and patterns
- Energy management (when high, when low)
- Nutrition habits and relationship with food
- Any chronic conditions relevant to advisory context

**relationship-coach** — Ask about:
- Key relationships (partner, family, close friends)
- Communication style in conflict
- Recurring interpersonal patterns
- Professional relationship dynamics

**philosopher** — Ask about:
- Core beliefs about meaning and purpose
- Ethical frameworks the user operates from
- Questions they return to again and again
- What they believe but cannot fully justify

**legal-counsel** — Ask about:
- Business structures, contracts, IP
- Any ongoing or recent legal matters
- Risk exposure in current ventures
- Legal questions they have been avoiding

### Completion Tracking

The coordinator maintains a completion status in `profile/domains.md` under a header `## Interview Completion`:

```
## Interview Completion
- [x] base.md — Session 1 (2026-03-01)
- [x] strategist — Session 2 (2026-03-03)
- [ ] psychologist — pending
- [ ] business-strategist — pending
...
```

When a member activates before their interview is complete, they prefix their response:
> "I don't have your full profile yet — I'm working from what we've covered so far. Once we complete my intake session, I'll know you much better."

### Output Format

Each member writes their intake to `profile/domains.md` under their section:

```markdown
## {member-name} Domain Profile
*Captured: {date}*

{Structured notes from the interview — facts, patterns, stated preferences}
```

Base identity goes to `profile/base.md`. Core values captured during strategist and philosopher interviews go to `profile/values.md`.

## Application Guide

### Scenario A: First Session (New User)

1. Coordinator greets user and explains the onboarding process (one paragraph, not a lecture)
2. Coordinator conducts base identity intake via direct conversation (10-15 min equivalent)
3. Coordinator writes `profile/base.md`
4. Coordinator notifies which member will conduct next domain interview
5. First domain interview begins if user has time; otherwise schedules for next session

### Scenario B: Resuming Onboarding Mid-Sequence

1. Coordinator reads completion status from `profile/domains.md`
2. Coordinator states which interviews are complete and which remain
3. Coordinator offers: continue with next interview, or use the team now and interview later
4. If user chooses to continue: route to next priority member for their intake segment
5. Member conducts intake, writes to `profile/domains.md`, updates completion status

### Scenario C: User Wants to Skip or Defer Interview

If user declines to complete a member's interview segment:
- Mark the segment as "deferred" in completion tracking, not "skipped"
- The relevant member operates with reduced context until the interview completes
- Do not pressure the user. State once: "I'll work with what I know for now. We can complete this whenever you're ready."

## Quality Checkpoints

- [ ] `profile/base.md` exists and contains all required fields after Session 1
- [ ] Completion tracker is accurate and up to date
- [ ] Each domain section in `profile/domains.md` is written by the appropriate member, not the coordinator
- [ ] No user-specific information is hardcoded in any agent .md file (profile-portability rule)
- [ ] Members operating before their interview flag the incomplete profile in their first response

## Examples

### Normal Case: Session 1 Base Intake

**Input**: New user, no profile exists

**Coordinator action**:
> "Welcome. Before our partners formally step in, I need to get to know some basics about you — about 10 minutes. This information will let everyone be genuinely helpful from day one."

Conducts structured intake → writes `profile/base.md` → updates completion tracker → introduces strategist for first domain interview

### Edge Case: User Adds Significant New Information Mid-Session

**Input**: User mentions mid-conversation they recently went through a major career change not captured in their profile

**Member action**: Pause advising, note the new information, flag to coordinator. Coordinator writes an update to the relevant profile section and marks it as "updated: {date}".

Do not silently absorb the new information without updating the profile.

### Rejection/Failure Case: User Refuses to Share Financial Information

**Input**: User says "I'd rather not discuss finances" during cfo intake

**cfo response**:
> "Understood. I'll flag that financial context is limited in your profile. When financial topics come up, I'll be more conservative in my analysis because I'm working with incomplete information. You can add this anytime."

Update completion tracker: "cfo — partial (financial data withheld by user, {date})"

Do not re-ask in the same session. Do not speculate about the user's finances.
