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

### Applying Managed Changes

- Preview the intended changes and apply the smallest target scope that covers them. Apply a parent directory only when the change requires it and its preview contains no unrelated changes.
- If `chezmoi apply` prompts because of local destination drift, stop and show the drift. Do not force an overwrite or retry with narrower paths merely to bypass the prompt; overwrite unrelated drift only when explicitly requested.
- Removing a source file does not guarantee removal of its destination. For intended deletions, use an explicit removal mechanism such as `remove_` or `.chezmoiremove`, preview it and verify the destination is absent afterwards. Do not add `exact_` solely to remove one stale file: it removes unmanaged entries more broadly. An empty `chezmoi diff` alone does not prove cleanup.

### Rename & Extension Changes

- When a managed target is renamed (including extension changes like `.json` -> `.jsonc`), do not assume chezmoi removes the old destination file.
- After applying, verify both paths explicitly:
  - New path exists and matches source
  - Old path no longer exists (or is intentionally kept)
- Use `chezmoi source-path <destination-path>` plus direct file checks (for example `ls`) to confirm path mapping and cleanup.

## Adding A New Tool

When adding configuration for a new tool:

- Keep it minimal at first; avoid capturing whole directories blindly.
- Add tool-specific guardrails and best practices to this file in the same PR when needed.
- Call out manual verification steps in the PR description.

## Ghost CLI

- Manage `@tryghost/ghst` through mise with an explicit version.
- Keep `~/.config/ghst/` out of chezmoi; it holds local site configuration and authentication material.
- Keep MCP registration in each client's configuration and credentials outside this repository.

## Handy Commands

```sh
chezmoi managed
chezmoi source-path ~/.config/zed/settings.json
chezmoi diff
chezmoi apply -n -v
chezmoi apply -v
git check-ignore -v <path>
```
