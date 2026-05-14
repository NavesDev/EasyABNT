# Contributing

## Git Standards

### Branches

Use short, lowercase branch names with hyphens:

```text
feature/unip-abnt
fix/plugin-manifest
docs/git-standards
chore/marketplace-entry
```

Recommended prefixes:

- `feature/` for new functionality.
- `fix/` for bug fixes.
- `docs/` for documentation-only changes.
- `chore/` for repository maintenance.
- `refactor/` for internal changes without behavior changes.
- `test/` for test-only changes.

### Commits

Use Conventional Commits:

```text
type(scope): short imperative summary
```

Examples:

```text
feat(unip-abnt): add institutional plugin scaffold
docs(readme): describe marketplace strategy
fix(manifest): update repository URL
chore(repo): add MIT license
```

Allowed types:

- `feat`: new user-facing behavior or plugin capability.
- `fix`: correction of existing behavior or metadata.
- `docs`: documentation changes.
- `style`: formatting-only changes.
- `refactor`: internal restructuring without behavior change.
- `test`: tests or validation fixtures.
- `chore`: maintenance, tooling, or repository setup.

Keep commits focused. Do not mix unrelated plugin changes, documentation rewrites, and formatting cleanup in the same commit.

### Pull Requests

Each pull request should include:

- What changed.
- Why it changed.
- How it was validated.
- Any ABNT or institutional source used for rule changes.
- Any known limitation, assumption, or pending follow-up.

For institutional plugins, include the institution name in the title or scope, for example:

```text
feat(unip-abnt): add UNIP document writing checklist
```

### Versioning

Use semantic versioning for plugin manifests:

- `MAJOR`: incompatible changes to plugin behavior, structure, or supported document contracts.
- `MINOR`: new skills, institutional rules, templates, or supported document types.
- `PATCH`: corrections, metadata updates, wording fixes, and small rule clarifications.

Institution-specific plugins should version independently from the generic `easy-abnt` plugin.

### Review Rules

- Do not invent ABNT rules or institutional requirements.
- Prefer references, manuals, or explicit user-provided rules for institution-specific behavior.
- Mark uncertain formatting rules as assumptions.
- Preserve existing user changes unless a task explicitly asks to replace them.
- Avoid destructive Git commands such as `git reset --hard` or forced checkout during contribution work.

### Validation

Before opening a pull request, run the relevant checks for touched files. At minimum:

```bash
python3 -m json.tool plugins/<plugin-name>/.codex-plugin/plugin.json
```

If marketplace files are changed, validate them too:

```bash
python3 -m json.tool claude-plugin/marketplace.json
```

Document any command that could not be run and why.
