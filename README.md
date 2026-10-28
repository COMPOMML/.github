# .github

Org-wide defaults for COMPOMML: issue forms (story, task, bug, epic, sprint close), the PR template and the reusable workflows. Repos without their own templates use these.

**This repo is public — never put anything sensitive here** (no client names, lab data, decks, results or internal paths).

## Reusable workflows

Call them from a repo's workflow with `uses: COMPOMML/.github/.github/workflows/<file>.yml@main`.

| Workflow | What it does |
|---|---|
| `python-ci.yml` | Byte-compiles every Python file in `src/ dev/ scripts/` (skips `dev/scripts_used/`, the dated history) |
| `gitleaks.yml` | gitleaks CLI scan of the full git history (a repo's `.gitleaks.toml` is picked up) |

Third-party actions are pinned to commit SHAs and CLI binaries are pinned by version + SHA-256.
Dependabot bumps the actions; bump the binary versions/checksums in the `env:` blocks by hand.
