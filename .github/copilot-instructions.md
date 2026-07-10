# Copilot code review instructions

This is a playground repository for experimenting with **semantic-release**. It contains
no application source code — only release automation config. Keep reviews focused on the
release setup, not on nonexistent application logic.

## What to check

- **Conventional Commits**: releases are driven entirely by commit messages
  (`@semantic-release/commit-analyzer`). Flag PR titles/commits that do not follow
  Conventional Commits (`fix:`, `feat:`, `feat!:` / `BREAKING CHANGE:`), since a
  malformed type silently produces no release or the wrong version bump.
- **`.releaserc.json`**: verify it stays valid JSON and that any branch or plugin change
  is internally consistent (e.g. a plugin referenced here is one semantic-release can
  resolve). `master` = stable, `develop` = prerelease.
- **`.github/workflows/release.yml`**: check that release triggers and the
  `npx semantic-release` invocation remain coherent, and that `GITHUB_TOKEN` is passed
  via the workflow secret (never a hardcoded token).

## What NOT to flag

- Missing tests, build step, or lint config — this repo intentionally has none.
- The minimal `README.md` — it is a deliberate placeholder.

## Security

- Reject any hardcoded token or secret. Authentication must use the Actions
  `GITHUB_TOKEN` secret only.
