---
name: linear
description: Manage Linear issues, projects, milestones and status updates through MCP, with automatic workflow transitions, evidence-based field inference and previewed prose. Use when creating, triaging or working on a Linear ticket, or when planning or reporting on a Linear project.
---

## When To Use This Skill

Use this skill for Linear work through connected MCP tools, including:

- discovering teams, projects, milestones, cycles and workflow states
- viewing, searching, creating and updating issues
- writing issue comments, project updates, milestone descriptions and documents
- keeping a linked ticket aligned with implementation, review and completion
- planning a project's milestones and reporting progress on it

## Core Rules

- Use Linear MCP tools for Linear operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in the global instructions.
- Treat a request to work on an identified ticket as authorisation to maintain its status and fields under the rules below. Do not ask again for routine field updates supported by that context.
- Read-only requests (viewing, summarising, reviewing or discussing a ticket) do not trigger status or field changes. An explicit request to update fields still applies.
- Keep updates scoped to the ticket being worked on. Related tickets, parent issues and project status do not automatically share its progress.
- Group fields belonging to the same event, such as starting work and claiming an unassigned ticket, into one update where supported.

## Field Writes And Prose Writes

The two kinds of write have different rules.

- Field writes cover status, assignee, project, milestone, priority, cycle, relations and link attachments. Apply them when the evidence below supports them, then report what changed so the user can correct it.
- Prose writes cover issue descriptions, comments, project descriptions, status updates, milestone descriptions and documents. Show the full draft and wait for approval before posting, every time, including edits to existing text. Approval covers that one text only; "post and move to Done" approves that comment and that transition, nothing later.
- Do not post prose and then offer to fix it. The preview is the review step.

## Automatic Workflow Transitions

Resolve states from the issue's team and its workflow conventions. The names below describe intent; do not assume literal names or IDs. If the matching state is missing or ambiguous, keep the current state and ask only when resolving it matters to the task. Do not create workflow states.

| Evidence | Action |
| --- | --- |
| The user picks up the ticket, or implementation or substantive investigation for it begins | Move an unstarted ticket to the team's active work state, such as In Progress. Do this at the start of work, not only in the final wrap-up. |
| The agreed scope is implemented, relevant checks pass (or an accepted validation limitation is documented) and a deliverable is available for review | Move to the team's review state, such as In Review. Honour any team requirement for a published, non-draft PR. A draft PR, partial fix or local changes unavailable to the reviewer are insufficient on their own. |
| Review feedback requires implementation changes and that work begins | Move back to the active work state if that matches the team's review workflow. Merely reading or discussing feedback does not trigger this. |
| The ticket's completion criteria are satisfied with observable evidence | Move to the completed state according to the team's convention. A merge is sufficient only when merge is the completion criterion; wait for the rollout, release or acceptance when that is what the ticket promises. |
| A dependency prevents further progress | Use the team's established blocked state or convention when known. Do not invent a status or treat the end of a session as a blocker. |

- Reassess at meaningful milestones during the task, including before handing work back. Do not wait for the user to request each transition.
- Preserve a status already appropriate to the work. Do not regress a ticket already in review just because a new session starts.
- Do not reopen completed or cancelled tickets, or cancel or mark duplicates, based on inference alone. Follow an explicit request or ask if the requested work conflicts with the terminal state. A cancellation carries a short comment saying why.
- If completion criteria are unclear, keep the last supported state and resolve the ambiguity instead of equating implementation finished with Done.

## Inferring Issue Fields

Use explicit user choices first, then established issue or team conventions and concrete task context. Preserve existing values unless the request or new evidence calls for a change. A blank field is not an obligation to guess.

For new issues or unset fields, use these rules:

| Field | Inference rule |
| --- | --- |
| Team | Use the identified issue's team. For creation, use an explicit repository-to-team mapping or a clearly applicable parent issue or project convention. No default team is configured here; ask when multiple teams plausibly own the work. Do not move an existing issue between teams by inference. |
| Assignee | When the user says they are picking up the work, or asks the agent to implement it on their behalf, assign an unassigned issue to that user once their Linear identity is verified. Use the authenticated viewer only when it represents the user, not a shared or service account. Preserve someone else's assignment unless a takeover or reassignment is explicit. Creating or reporting a ticket alone does not make the user its owner. |
| Project | Use an explicit project, a documented repository mapping or a parent issue's project when the new work clearly belongs to the same scope. Verify that the project is applicable to the target team. A similar name or the fact that a project is active is insufficient; leave unset or ask when multiple projects fit. |
| Milestone | When the issue sits in a project with milestones, place it in the milestone the user names or the phase its scope clearly fits. Leave unset and ask when neither is clear. Do not move an issue between milestones by inference; the user reschedules by hand. |
| Relations | Record blocking and related relations when the user maps dependencies, or when a ticket is split from, unblocks or supersedes another. Relations are append-only in most tools, so add only what is intended and remove only when asked. |
| Priority | Infer from impact, urgency, affected users, deadlines and work being blocked, using the team's rubric where available. Use the fallback below only when the evidence supports it. Starting work does not itself increase priority. |
| Cycle and due date | Use an explicit scheduling commitment or established team rule. Do not infer the current cycle or invent a deadline merely because work starts now. |
| Labels | Reuse existing labels only when the issue clearly matches their meaning. Do not create new ones. |

Fallback priority rubric:

- Urgent: an active critical incident or immediate severe impact requiring interruption of other work.
- High: significant impact, a pressing deadline or a blocker for important committed work.
- Medium: routine planned work with clear value and no evidence of heightened urgency.
- Low: explicitly deferrable polish or minor inconvenience with a practical workaround.
- No priority: insufficient evidence to rank the work. Do not silently turn unknown priority into Medium.

Use the tool's documented priority encoding. Do not inherit a parent's priority automatically; assess the specific issue's impact.

Ask a concise, preferably structured question when competing interpretations would materially change ownership, routing, urgency or workflow. Offer the plausible choices and the reason for the recommendation. Continue independent work and apply unambiguous fields while an answer is pending; leave uncertain optional fields unchanged rather than blocking the whole task.

## Titles

- A title is a short summary. Details belong in the description. A title that stacks several outcomes usually means the issue needs splitting.
- Prefer an imperative that names the outcome, such as "Upgrade the ingress controller before the next cluster upgrade" or "Group deployment logs by stage".
- Bug titles start with "Fix" and name the symptom, not the diagnosis: "Fix database proxy outages during node rotations", not "Database proxy pods are evicted during node rotations" and not "Fix the database proxy's PodDisruptionBudget". Use "Investigate ..." only when the ticket's outcome is findings rather than a fix.

## Descriptions

- A description holds the problem, scope, constraints, acceptance criteria and durable context. It is the part a reader trusts to still be true later.
- Use `##` headings when they make the issue easier to scan. Common sections are Scope, Approach, Notes, Out of scope and References.
- When editing, preserve the existing structure, acceptance criteria and links. Prefer partial edits where the tool supports them; replace the whole description only for a rewrite the user has approved.
- Leave out bookkeeping and provenance: which ticket this was split from, which ticket comes next on the board, or earlier mistakes that have since been corrected. The project view already shows sequence, and the description should not read as a session transcript.
- Attach pull requests to the issue as link attachments (or through the GitHub integration) instead of pasting PR URLs into the text. Every PR belongs to an issue; do not leave orphans.

## Comments

- A comment adds new information: a finding, a decision, an outcome, what was verified and any remaining limitation. It does not restate the description or narrate edits. When the description holds the problem, the comment holds the solution or the result.
- Do not list PRs that are already attached to the issue. When a PR must be mentioned, link it inline within the sentence.
- Write for people. Plain, readable English in short paragraphs, not dense blocks. Tables are welcome when they structure information.
- Comment at meaningful points, such as a decision, a blocker, a review handoff or completion. Do not post a comment that only says what the status change already says, and do not report progress on an environment nobody is waiting on.

## Issue Links And References

- In paragraphs, use a Markdown link with the issue key as its label, such as `[ENG-123](<issue URL>)`. A bare key inline renders as a chip that breaks the reading flow, so do not use bare keys, inline code or bare URLs in prose. Use the URL returned by Linear; do not invent workspace slugs.
- Reference sections sit at the end of a description or project text under `##` headings, in this order:
  - `## Related Issues`: a deduplicated list of bare issue keys, one per item.
  - `## Related Projects`: a list of linked project titles, with a short note on the relationship where it helps.
  - `## References`: a list of other supporting links, such as Slack threads, documents, dashboards or upstream issues.
- Omit empty sections. Extend an equivalent existing section rather than adding a second one.
- Use linked issue keys in conversational updates too, without adding a reference section to every short reply.

## Projects, Milestones And Status Updates

- Milestone names are prefixed `M1`, `M2` and so on, followed by a short outcome, such as "M3: Failed deploys show their cause". Each milestone should end in something a person experiences, not a layer of plumbing.
- The user sets and moves milestone target dates and cycles. Do not set or shift them by inference.
- Keep the project description current when the plan changes. The description, title and reference conventions above apply to project text as well.
- Post a status update when a milestone completes or the plan changes, not on a schedule and not for routine progress. Write it for teammates and a manager who do not follow the day to day: lead with the change in one sentence, then what it means, then what is still open. Outcomes over technical detail, plain language, nothing the issues or the plan already show, and no bragging about hitting dates. Set the health honestly.
- Prefer Linear documents over repository proposals for shared context, and attach them to the project they support.

## Working Pattern

1. Identify the ticket from an explicit key or URL, an existing task link or an unambiguous branch or PR association. Search when necessary; do not choose between plausible matches by title similarity alone. Before creating an issue, check for an existing match when the context suggests one may already exist.
2. Read the current issue, including fields and relevant acceptance criteria or recent decisions. Discover only the team states, users, projects or other context needed for this operation; reuse verified context within the task.
3. Apply the transition and field rules above. Draft any prose and show it before posting. Refresh the issue before writing if work has continued since the last read. Respect intervening edits and integration-driven status changes; send only intended fields, not a stale copy of the whole issue.
4. Confirm the changed fields from the mutation response or a follow-up read. If a write times out or returns an uncertain result, read before retrying, especially for issue or comment creation. If the connection remains unavailable, stop retrying, continue independent work and report the unapplied update without claiming success.

## Authentication

Use the current client's connected Linear MCP tools and authentication flow. If the connection is unavailable or unauthenticated, use that client's setup guidance.

Do not store Linear API tokens in this repo. If token-based auth is needed, keep it in the local environment or the client's credential store, not chezmoi source.

## Tool Scope

Expect Linear MCP tools to cover issues, comments, projects, milestones, status updates, teams, users, cycles and documents.

Prefer discovering available tools from the connected MCP server instead of assuming exact tool names.

## Known Caveats

- Linear identifiers can be either issue keys (for example `ENG-123`) or internal IDs depending on the tool, so confirm which form a tool expects.
- Team-specific workflow state names can differ, so resolve state choices from the target team before updating status.
