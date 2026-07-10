# CLAUDE.md

## Overview

Playground repository for experimenting with [semantic-release](https://semantic-release.gitbook.io/).
It has no application source code — it exists only to try out release automation:
version bumping, changelog/release-note generation, and GitHub Release creation driven
by commit messages. Do not treat this as a library or service.

## Key files

- `.releaserc.json` — semantic-release configuration. Defines the release branches
  (`master` = stable, `develop` = prerelease) and the plugin chain
  (`@semantic-release/changelog`, `commit-analyzer`, `release-notes-generator`,
  `@semantic-release/github`).
- `.github/workflows/release.yml` — CI workflow. Runs `npx semantic-release` on pushes
  to `master` and `develop` (and on `repository_dispatch`).
- `README.md` — placeholder only.

## Commit conventions (most important)

Releases are fully driven by commit messages via `@semantic-release/commit-analyzer`,
so [Conventional Commits](https://www.conventionalcommits.org/) are mandatory here — the
commit type is what decides whether (and how) a release happens:

- `fix:` → patch release.
- `feat:` → minor release.
- `feat!:` / `BREAKING CHANGE:` footer → major release.
- `chore:`, `docs:`, `ci:`, etc. → no release.

A malformed commit message means no release is produced, so verify the type before committing.

## Branching / release model

- `master`: stable releases.
- `develop`: prerelease channel (`"prerelease": true` in `.releaserc.json`).
- Pushing to either branch triggers the release workflow.

## Testing / verification

There are no tests, build step, or lint config. To verify a change, observe the release
workflow run in GitHub Actions after pushing and confirm the expected release (or the
expected "no release") occurred.

## Security

- Never commit tokens or secrets. The workflow authenticates with the built-in
  `GITHUB_TOKEN` GitHub Actions secret only.

## Updating this file

Update this file when the release configuration changes — e.g. branches, the plugin
chain in `.releaserc.json`, or the release workflow triggers.
