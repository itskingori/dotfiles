# Project and discovery workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

## Check auth state

```bash
acli jira auth status
```

## Authenticate when needed

```bash
acli jira auth login --web
```

## Discover projects

```bash
acli jira project list --limit 50 --json
acli jira project view --key "TEAM" --json
```

## Discover and inspect work items

```bash
acli jira workitem search --jql "project = TEAM AND statusCategory != Done" --limit 50 --json
acli jira workitem view TEAM-123 --fields key,summary,status,assignee,description --json
```
