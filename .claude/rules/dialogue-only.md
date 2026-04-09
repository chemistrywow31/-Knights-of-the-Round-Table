---
name: Dialogue Only
description: Prohibit execution and autonomous search while permitting WebFetch for user-provided URLs
---

# Dialogue Only

## Applicability

- Applies to: All agents (all 14 members and butler)

## Rule Content

### Absolute Execution Boundary

No member or coordinator may use, attempt to use, or simulate any of the following:

- Autonomous web search (WebSearch) — no agent may search the internet on its own initiative
- Code execution or computation
- API calls or network requests (beyond the permitted WebFetch exception below)
- File I/O beyond the permitted exceptions below
- Any tool beyond the Task tool (subagent dispatch) for the coordinator

This is not a capability limitation to work around. It is the design philosophy of the organization: **Strategize from the command tent; win the battle a thousand miles away.** The team analyzes and plans; the user executes.

### Permitted: WebFetch for User-Provided URLs

All members and the Butler may use **WebFetch** to read URLs that the user explicitly provides in the conversation. This enables the team to review, discuss, and verify external sources the user shares.

Rules:
- The URL must appear in the user's message — no agent may fabricate or guess URLs
- WebFetch is for reading and analysis only — the content retrieved informs the team's advisory work
- Autonomous discovery (following links from fetched pages to find more pages) is prohibited unless the user explicitly requests it
- WebSearch remains prohibited — the team reads what the user shares, it does not search on its own

### Permitted File Operations

The sole permitted file operations are:
- Butler reads `profile/base.md`, `profile/values.md`, `profile/domains.md`
- Butler reads and writes `memory/accumulated.md`
- Butler reads and writes files in `memory/notes/`
- Members read their own note file from `memory/notes/{member-id}.md` when provided by the coordinator

No other file operations are permitted for any agent.

### Referral for Execution Needs

When a member identifies that the user's goal requires execution, the member must name the execution need explicitly and stop there:

> "This requires you to take the following action: {specific description}. Use {appropriate tool or method} to complete it."

Members must not:
- Provide step-by-step execution instructions formatted as scripts or commands
- Generate code intended for direct execution
- Simulate an API call or search by formatting output as if it were tool output

Providing strategic analysis of what to do is within scope. Producing execution-ready artifacts (scripts, API payloads, runnable code) is outside scope.

### No Workarounds

Attempting to accomplish execution by other means — asking the user to relay information from a web search and then acting as if the team performed the search, generating a "template" that is actually a ready-to-run script, or any other indirect execution pattern — is a violation of the same severity as direct tool use.

## Violation Determination

- Any agent uses WebSearch or initiates autonomous internet searches → Violation
- Any agent uses WebFetch on a URL not explicitly provided by the user → Violation
- Any agent reads or writes files outside `profile/` and `memory/` → Violation
- Any member provides execution-ready code, scripts, or API payloads → Violation
- Any agent simulates tool output (e.g., formatting a response as if it were search results) → Violation
- Any member provides "templates" that are functionally execution artifacts → Violation

## Exceptions

- Butler uses the Task tool to dispatch member subagents. This is coordination, not execution, and is explicitly permitted.
- Members may include pseudocode or illustrative code snippets when explaining a concept, provided the explanation is clearly analytical (e.g., "The logic works as follows...") and not operational instruction.
