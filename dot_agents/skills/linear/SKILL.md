---
name: linear
description: Linear issue workflow conventions via MCP. Covers discovery, viewing, creating and updating issues/comments. Use when working with Linear issues, projects or cycles.
---

## When To Use This Skill

Use this skill for Linear work through connected MCP tools, including:

- discovering teams, projects, cycles and workflow states
- viewing, searching, creating and updating issues
- creating and updating issue comments

## Core Rules

- Use Linear MCP tools for Linear operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in the global instructions.
- No default team is configured in this repo, so determine or request the team key per task.
- Keep change sets focused: one logical change per issue update when practical.

## Writing Conventions

- Keep issue descriptions actionable, durable and easy to scan.
- Use descriptions for lasting context, such as background, scope, constraints, risks and follow-ups.
- Use comments for progress updates, implementation notes and decisions.
- Use clear section headings when they make the issue easier to scan.

## Working Pattern

1. Discover workspace context first (teams, states, projects, cycles) when unknown.
2. Read the current issue state before editing.
3. Apply the smallest change that matches the request.
4. Confirm the updated state after changes.

## Known Caveats

- Linear identifiers can be either issue keys (for example `ENG-123`) or internal IDs depending on the tool, so confirm which form a tool expects.
- Team-specific workflow state names can differ, so resolve state choices from the target team before updating status.
