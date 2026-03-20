# Issue create and edit workflows

Use these patterns to create and update issues with `gh`.

## Create an issue

```bash
gh issue create \
  --title "Clarify GitHub skill workflow boundaries" \
  --body-file "dot_config/opencode/skills/github/examples/issue-body-structured.md"
```

## Edit an existing issue

```bash
gh issue edit 123 \
  --title "Refine GitHub skill workflow boundaries" \
  --body-file "dot_config/opencode/skills/github/examples/issue-body-structured.md"
```

## Use stdin for one-off issue content

```bash
gh issue edit 123 --body-file - <<'EOF'
Clarifies workflow boundaries for the GitHub skill.

### Scope
- Keep nuanced PR writing guidance in the main skill file
- Move command recipes to dedicated workflow examples
EOF
```
