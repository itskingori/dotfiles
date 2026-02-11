# AGENTS.md (Repo-Local)

Public chezmoi dotfiles. Keep changes reproducible and safe.

## Non-Negotiables

- This repo is public: do not commit secrets of any kind (even encrypted).
- Prefer repeatable configuration over machine-specific state.
- Keep changes small and reviewable.

## What Counts As A Secret (Examples)

- API keys, tokens, cookies, client secrets
- SSH private keys, `known_hosts`, agent sockets
- Any credential material, recovery codes, license keys
- Session/state/cache/history/log/backup artifacts unless explicitly intended and reviewed

If something feels secret-ish, do not add it. Prefer referencing an external secret manager (for example, 1Password) at runtime.

## Chezmoi Basics

- This repo is chezmoi source state; it may not resemble destination paths.
- Use these commands to understand mappings:
  - `chezmoi managed`
  - `chezmoi source-path <destination-path>`
- `private_` files preserve private permissions; treat them as sensitive-by-default and review contents.

## Change Workflow (Preferred)

- Before committing:
  - Ensure the PR diff contains only intended files.
  - Run `git check-ignore -v <path>` when something disappears unexpectedly.
- Before applying:
  - `chezmoi diff` (or `chezmoi apply -n -v` if unsure)
- After merging:
  - `chezmoi apply -v`
  - `chezmoi diff` should be empty

## Adding A New Tool

When adding configuration for a new tool:

- Keep it minimal at first; avoid capturing whole directories blindly.
- Add tool-specific guardrails and best practices to this file in the same PR when needed.
- Call out manual verification steps in the PR description.

## Handy Commands

```sh
chezmoi managed
chezmoi source-path ~/.config/zed/settings.json
chezmoi diff
chezmoi apply -n -v
chezmoi apply -v
git check-ignore -v <path>
```
