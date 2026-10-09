# sepsis

Early-stage project: no application code yet. Update this file once the stack is chosen
(build, test, lint and dev-server commands go in **Commands** below).

## Commands

_None yet._ Add them here as soon as they exist, e.g.:

- Test: `TBD`
- Lint / typecheck: `TBD`
- Dev server: `TBD`

## Clinical data

This project is about sepsis, so treat any patient-level data as PHI:

- Never commit real patient data. Raw and interim data stay under `data/raw/` and
  `data/interim/`, which are gitignored. Use synthetic or de-identified fixtures in tests.
- Don't paste real patient records into prompts, issues, PR descriptions or logs.
- Clinical logic (scores, thresholds, alerts) needs a test that cites its source
  (e.g. Sepsis-3 / qSOFA definitions) next to the assertion.

## Repo tooling (`.claude/`)

- **Guard hooks** (`.claude/hooks/`, wired in `.claude/settings.json`) run on every
  matching tool call:
  - `guard-delete-outside`: no deletes outside the repo.
  - `guard-protected-push`: no direct/force pushes to protected branches.
  - `guard-secrets`: no reading `.env` and other secret files.
  - `guard-key-literals`: no API keys written into files.
  - `guard-worktree-path`: git worktrees only under `.claude/worktrees/`.
  - `cleanup-wt` runs at session start and prunes stale worktrees.

  They fail open on internal errors. Don't work around a block; fix the command or ask.
- **Workflow skills**: `super-board` (issue board / waves), `super-build`, `super-qa`,
  `super-review`, `super-collect`, `ui-refine-loop`, `visual`, `git-sync`. Their docs
  are in `.claude/skills/<name>/SKILL.md`.
- Worktrees live only under `.claude/worktrees/` (gitignored). Never edit the main
  checkout from a worker.
- `.claude/settings.local.json` holds machine-local overrides and cached e2e test
  credentials. It is gitignored; never commit it.

## Conventions

- Work on a branch and open a PR; don't push to `main` directly.
- Hooks require `python3` on PATH (Python 3.14 on this machine).
