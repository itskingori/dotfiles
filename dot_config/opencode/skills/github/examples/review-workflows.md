# Review workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

Use these commands to inspect PR and issue state before writing updates.

## View PR metadata

```bash
gh pr view 40 --json title,body,state,isDraft,baseRefName,headRefName,url
```

## View PR checks

```bash
gh pr checks 40
```

## View PR diff

```bash
gh pr diff 40
```

## View PR comments

```bash
gh pr view 40 --comments
```

## View issue metadata

```bash
gh issue view 123 --json title,body,state,labels,assignees,url
```
