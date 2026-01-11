# Ship

Create a PR for current changes with version bump and README update.

## Workflow

1. **Check for changes**: Run `git status` and `git diff` to understand what changed
2. **Update README.md**: If any skill content changed, update the corresponding skill description in README
3. **Bump version**: Increment version in `.claude-plugin/plugin.json` (patch for fixes, minor for features)
4. **Create branch**: `git checkout -b <descriptive-branch-name>`
5. **Commit**: Stage and commit with a clear message summarizing the changes
6. **Push**: `git push -u origin <branch-name>`
7. **Create PR**: Use `gh pr create` with summary and test plan

## Arguments

$ARGUMENTS - Optional description of what changed (used for branch name and commit message)
