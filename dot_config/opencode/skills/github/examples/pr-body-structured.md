Expands the GitHub skill into a workflow-first playbook that covers authoring and review workflows in `gh`. Adds practical command patterns for pull requests, issues, and comments while keeping repository-specific writing conventions intact.

### Motivation
- The existing skill is PR-heavy and does not fully cover issue and comment workflows.
- Workflow coverage should reflect the skill description, which says it applies to any GitHub interaction.

### Changes
- Reframes the skill into clear sections for auth, input modes, command patterns, and caveats.
- Adds deterministic body-formatting guidance using `--body-file` and quoted heredocs.
- Adds examples for reusable PR, issue, and comment markdown bodies.

### Testing
- I validated command patterns against `gh --help` output for PR, issue, and comment operations.
- I reviewed example files to ensure they are copy-paste friendly and aligned with current conventions.

### Related
- https://github.com/itskingori/dotfiles/pull/39
