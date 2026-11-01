# tasks/lessons.md — RocketEdge/ibc

## 2026-11-01 — Upstream `.gitignore` hides dotfiles

**Pattern:** upstream ignores `.*`, which would have excluded `.github/` (workflows, CODEOWNERS,
Dependabot) from git without any error.

**Rule:** after adding `.github/` to a forked repository, run `git check-ignore -v .github/workflows/build.yml`
and negate the pattern if needed.
