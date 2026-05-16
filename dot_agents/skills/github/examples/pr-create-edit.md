# PR create and edit workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

Use these patterns to create and update pull requests with `gh`.

## Create a draft PR

```bash
gh pr create \
  --draft \
  --title "Add workflow-first GitHub skill guidance" \
  --body-file - <<'EOF'
Body text.
EOF
```

## Create a ready-for-review PR

```bash
gh pr create \
  --title "Add workflow-first GitHub skill guidance" \
  --body-file - <<'EOF'
Body text.
EOF
```

## Update an existing PR title and body

```bash
gh pr edit 40 \
  --title "Refine GitHub skill workflow guidance" \
  --body-file - <<'EOF'
Body text.
EOF
```

## Safe stdin pattern for generated Markdown

```bash
gh pr edit 40 --body-file - <<'EOF'
Body text.
EOF
```

## Notes

- `gh pr create --dry-run` can still push branch changes in some flows, so do not assume it is side-effect free.
- `gh pr create` may prompt for push or fork when branch tracking is missing. Use `--head` when deterministic behaviour is required.
