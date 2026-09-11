---
name: linear
description: Manage Linear issues through MCP, including automatic workflow transitions and evidence-based metadata inference. Use when creating, triaging or working on a Linear ticket, as well as for Linear projects, cycles and comments.
---

## When To Use This Skill

Use this skill for Linear work through connected MCP tools, including:

- discovering teams, projects, cycles and workflow states
- viewing, searching, creating and updating issues
- creating and updating issue comments
- keeping a linked ticket aligned with implementation, review and completion

## Core Rules

- Use Linear MCP tools for Linear operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in the global instructions.
- Treat a request to work on an identified ticket as authorisation to maintain its status and infer metadata under the rules below. Do not ask again for routine updates supported by that context.
- Read-only requests (viewing, summarising, reviewing or discussing a ticket) do not trigger status or metadata changes. An explicit request to update fields still applies.
- Keep updates scoped to the ticket being worked on. Related tickets, parent issues and project status do not automatically share its progress.
- Group fields belonging to the same event, such as starting work and claiming an unassigned ticket, into one update where supported.

## Automatic Workflow Transitions

Resolve states from the issue's team and its workflow conventions. The names below describe intent; do not assume literal names or IDs. If the matching state is missing or ambiguous, keep the current state and ask only when resolving it matters to the task. Do not create workflow states.

| Evidence | Action |
| --- | --- |
| The user picks up the ticket, or implementation or substantive investigation for it begins | Move an unstarted ticket to the team's active work state, such as In Progress. Do this at the start of work, not only in the final wrap-up. |
| The agreed scope is implemented, relevant checks pass (or an accepted validation limitation is documented) and a deliverable is available for review | Move to the team's review state, such as In Review. Honour any team requirement for a published, non-draft PR. A draft PR, partial fix or local changes unavailable to the reviewer are insufficient on their own. |
| Review feedback requires implementation changes and that work begins | Move back to the active work state if that matches the team's review workflow. Merely reading or discussing feedback does not trigger this. |
| The ticket's completion criteria are satisfied with observable evidence | Move to the completed state according to the team's convention. A merge is sufficient only when merge is the completion criterion; wait for deployment or acceptance when required. |
| A dependency prevents further progress | Use the team's established blocked state or convention when known. Do not invent a status or treat the end of a session as a blocker. |

- Reassess at meaningful milestones during the task, including before handing work back. Do not wait for the user to request each transition.
- Preserve a status already appropriate to the work. Do not regress a ticket already in review just because a new session starts.
- Do not reopen completed or cancelled tickets, or cancel or mark duplicates, based on inference alone. Follow an explicit request or ask if the requested work conflicts with the terminal state.
- If completion criteria are unclear, keep the last supported state and resolve the ambiguity instead of equating implementation finished with Done.

## Inferring Issue Fields

Use explicit user choices first, then established issue or team conventions and concrete task context. Preserve existing values unless the request or new evidence calls for a change. A blank field is not an obligation to guess.

For new issues or unset fields, use these rules:

| Field | Inference rule |
| --- | --- |
| Team | Use the identified issue's team. For creation, use an explicit repository-to-team mapping or a clearly applicable parent issue or project convention. No default team is configured here; ask when multiple teams plausibly own the work. Do not move an existing issue between teams by inference. |
| Assignee | When the user says they are picking up the work, or asks the agent to implement it on their behalf, assign an unassigned issue to that user once their Linear identity is verified. Use the authenticated viewer only when it represents the user, not a shared or service account. Preserve someone else's assignment unless a takeover or reassignment is explicit. Creating or reporting a ticket alone does not make the user its owner. |
| Project | Use an explicit project, a documented repository mapping or a parent issue's project when the new work clearly belongs to the same scope. Verify that the project is applicable to the target team. A similar name or the fact that a project is active is insufficient; leave unset or ask when multiple projects fit. |
| Priority | Infer from impact, urgency, affected users, deadlines and work being blocked, using the team's rubric where available. Use the fallback below only when the evidence supports it. Starting work does not itself increase priority. |
| Labels | Reuse existing labels when the issue clearly matches their meaning. Preserve unrelated labels and do not create new taxonomy just to classify one issue. |
| Cycle and due date | Use an explicit scheduling commitment or established team rule. Do not infer the current cycle or invent a deadline merely because work starts now. |

Fallback priority rubric:

- Urgent: an active critical incident or immediate severe impact requiring interruption of other work.
- High: significant impact, a pressing deadline or a blocker for important committed work.
- Normal: routine planned work with clear value and no evidence of heightened urgency.
- Low: explicitly deferrable polish or minor inconvenience with a practical workaround.
- No priority: insufficient evidence to rank the work. Do not silently turn unknown priority into Normal.

Resolve the tool's accepted priority values rather than assuming a numeric encoding. Do not inherit a parent's priority automatically; assess the specific issue's impact.

Ask a concise, preferably structured question when competing interpretations would materially change ownership, routing, urgency or workflow. Offer the plausible choices and the reason for the recommendation. Continue independent work and apply unambiguous fields while an answer is pending; leave uncertain optional fields unchanged rather than blocking the whole task. Briefly report inferred changes so the user can correct them.

## Writing Conventions

- Keep issue descriptions actionable, durable and easy to scan.
- Use descriptions for lasting context, such as background, scope, constraints, risks and follow-ups.
- Use comments for progress updates, implementation notes and decisions.
- Use clear section headings when they make the issue easier to scan.
- Preserve existing description structure, acceptance criteria and useful links when editing. Add durable discoveries without replacing the issue with a session transcript.
- Post comments only when requested or already authorised by the user. When authorised, comment on material decisions, blockers or review handoffs; avoid narrating every edit or repeating a status-only change. Include the relevant deliverable link, validation result and remaining limitation when useful.

### Issue Links And References

- In paragraphs, use a Markdown link with the issue key as its label, such as `[ENG-123](<verified issue URL>)`. Do not wrap issue keys in inline code or use bare URLs in prose. Use the canonical URL returned by Linear or supplied in verified context; do not invent workspace slugs or URLs.
- In Linear descriptions and comments that reference other issues, collect those issues under `### Related` as a deduplicated list of bare issue URLs, one per list item. Keep inline links where they explain the relationship. Use `### References` for other supporting links, also as a list, after Related. Omit empty sections and preserve equivalent existing sections rather than duplicating them.
- Use linked issue keys in conversational updates too, without adding a reference section to every short reply. When writing for another platform, follow its section conventions; GitHub places Linear links under References.

## Working Pattern

1. Identify the ticket from an explicit key or URL, an existing task link or an unambiguous branch/PR association. Search when necessary; do not choose between plausible matches by title similarity alone. Before creating an issue, check for an existing match when the context suggests one may already exist.
2. Read the current issue, including fields and relevant acceptance criteria or recent decisions. Discover only the team states, users, projects or other context needed for this operation; reuse verified context within the task.
3. Apply the milestone and field rules above. Refresh the issue before writing if work has continued since the last read. Respect intervening edits and existing integration-driven status changes; send only intended fields, not a stale copy of the whole issue.
4. Confirm the changed fields from the mutation response or a follow-up read. If a write times out or returns an uncertain result, read before retrying, especially for issue or comment creation. If the connection remains unavailable, stop retrying, continue independent work and report the unapplied update without claiming success.

## Authentication

Use the current client's connected Linear MCP tools and authentication flow. If the connection is unavailable or unauthenticated, use that client's setup guidance.

Do not store Linear API tokens in this repo. If token-based auth is needed, keep it in the local environment or the client's credential store, not chezmoi source.

## Tool Scope

Expect Linear MCP tools to cover issues, comments, projects, teams, users, cycles and documents.

Prefer discovering available tools from the connected MCP server instead of assuming exact tool names.

## Known Caveats

- Linear identifiers can be either issue keys (for example `ENG-123`) or internal IDs depending on the tool, so confirm which form a tool expects.
- Team-specific workflow state names can differ, so resolve state choices from the target team before updating status.
