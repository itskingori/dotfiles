# PR create and edit workflows

Use these patterns to create and update pull requests with `gh`.

## Create a draft PR

```bash
gh pr create \
  --draft \
  --title "Add workflow-first GitHub skill guidance" \
  --body-file "dot_config/opencode/skills/github/examples/pr-body-structured.md"
```

## Create a ready-for-review PR

```bash
gh pr create \
  --title "Add workflow-first GitHub skill guidance" \
  --body-file "dot_config/opencode/skills/github/examples/pr-body-structured.md"
```

## Update an existing PR title and body

```bash
gh pr edit 40 \
  --title "Refine GitHub skill workflow guidance" \
  --body-file "dot_config/opencode/skills/github/examples/pr-body-structured.md"
```

## Safe stdin pattern for generated Markdown

```bash
gh pr edit 40 --body-file - <<'EOF'
Updates the GitHub skill to keep nuanced writing guidance central while moving command recipes into examples.

### Changes
- Preserves PR writing conventions and section rules
- Moves command-heavy workflows into dedicated example files
EOF
```

## Notes

- `gh pr create --dry-run` can still push branch changes in some flows, so do not assume it is side-effect free.
- `gh pr create` may prompt for push or fork when branch tracking is missing. Use `--head` when deterministic behaviour is required.
