# Claude Code Guidelines

## Publishing & review workflow

This repository deploys to **public GitHub Pages on every push to `main`**. Treat
`main` as production. Nothing should reach it without Leo's explicit approval.

- For all changes, create a branch and write clear, scoped commits.
- Open PRs for Leo to review. PRs are for **human review** — do not rely on
  automated reviewers, and do not merge on a timer.
- **Never merge to `main` without Leo's explicit say-so.** Likewise, never push
  placeholder, filler, or unreviewed content in a way that could publish.
- Stacked PRs are fine: branch off a feature branch for follow-up work (e.g.
  content changes on top of a redesign), and merge down the stack only once Leo
  approves each layer.
- Pushing a feature branch and opening a PR is fine; it does not deploy. Only
  `main` deploys.
- Address PR comments by fixing valid ones or responding to invalid ones.
- Do not deploy or merge autonomously. Wait for Leo.
