# .github — org-wide defaults (PUBLIC repo)

Issue forms, PR template, org profile and the reusable workflows every COMPOMML repo calls (`python-ci`, `gitleaks`). This repo is public: never put secrets, client names, lab data, internal paths or plans here.

## Commands
- Lint workflows: `actionlint`
- Pin every third-party action to a full commit SHA with the version in a comment.

<!-- team-rules:start -->
## COMPO team rules (synced from COMPOMML/docs/agents/team-rules.md — edit there, not here)

**Work**
- Start from a GitHub issue with acceptance criteria. If there is none or it is vague, stop and ask instead of guessing.
- One issue → one small PR to `main` (squash merge). Conventional commits (`feat:`, `fix:`, `chore:`, `docs:`, `ci:`…). Put `Closes COMPOMML/<repo>#<n>` in the PR body.
- CI must be green before merge (the Free plan can't enforce it — we do). Don't merge your own PR unless the human asked; `/wave` PRs are the exception: its Codex merger agent merges them under the checks in the wave skill (add `manual` to `/wave` to merge them yourself).
- Never add Claude attribution: no `Co-Authored-By: Claude` trailer, no "Generated with Claude Code" line in PRs, issues or comments.
- Ask before anything destructive or hard to undo: force-push, history rewrite, deleting branches/data, changing org or repo settings.
- English for everything: code, comments, commits, issues, PRs and docs.
- Runner minutes are limited (Free plan: 2,000 a month for private repos). Run the repo's checks locally before pushing and push when they pass, not after every work-in-progress commit.

**COMPO rules**
- **Client data stays private.** Lab data, decks, the reference model, reports and measured values live only in the private repos. Nothing from them goes into `.github` (public), an issue title visible outside the org, or a commit to a public place.
- **Never start a solver.** Only a human presses the button that launches LS-DYNA (`RUNNER.run_jobs(confirmed=True)`, from the OPTI screen). Agents write code, decks and batch files and leave every run to the human.
- **Never write into the curated LS-DYNA tree** (`000_Final_Version`). COMPO reads deliveries from it and writes only into its own numbered folders.
- **Paths are decided in `compo_paths.py` only** (CORE). No module works out a path for itself.
- **Results and lab data are never committed:** `01_CAL_OUT` … `05_REPO_OUT`, `00_MATERIALS/*`, built `.exe` files.
- **Every change ships with its patch script** in the owning repo's `dev/scripts_used/patches/` (dated `YYYY-MM-DD_<what>.py`), as in the handover.
- **Cross-repo order:** `CORE` first (and backward compatible with the modules on `main`), then the modules in chain order CAL → ORGA → RUNNER → OPTI → REPO.

**Context** — plan and architecture live in `COMPOMML/docs` (`plan.md`, `product/scope.md`, `architecture/`, `decisions/`). The handover notes (`info/CLAUDE.md`, `info/HANDOVER_2026-10-02.md`) live in `COMPOMML/CORE`. Board: https://github.com/orgs/COMPOMML/projects/1. Read only the sections you need.

**Model routing (save tokens)** — sessions run on Sonnet by default. Delegate:
- `scout` (Haiku): searching code, reading CI logs, listing issues/PRs, summarizing long files or diffs.
- `tech-lead` (Opus): splitting an issue into tasks, design decisions, final review against acceptance criteria.
- `security-reviewer` (Opus): before merging anything that touches client data, the solver launch, secrets or CI workflows.
- `cal-workbook-auditor`, `compo-run-checker` (Sonnet, read-only): independent audit after a CAL change, and after an ORGA, RUNNER or OPTI change.
- Implementation agents (Sonnet): `compo-dev`, `infra-dev`, `test-writer`.
- Don't use Opus for routine coding. Don't read whole large files when grep will do. Keep at most 2–3 agents in parallel.
- Codex sessions: the agents above are Claude-only; do the work directly and keep to the same rules.
<!-- team-rules:end -->
