# Contributing

This is a solo project, but it follows the same workflow a team would.

## Branches (GitHub Flow)
- `main` always builds and passes tests. Nothing is committed to it directly.
- One short-lived branch per issue, merged within a few days:
  - `feature/<issue>-<short-name>` e.g. `feature/3-easter-calculator`
  - `fix/<issue>-<short-name>` e.g. `fix/12-holiday-off-by-one`
- The branch is deleted after merging.

## Commits
- Imperative mood, short subject: `Add Easter calculator`
- Reference the issue: `Add Easter calculator (#3)`

## Pull requests
- Use the PR template and link the issue (`Closes #3`)
- CI must pass before merging
- Squash-merge into `main`

## Releases
- Tagged with semantic versions: `v0.1.0`
- Changes listed in `CHANGELOG.md`
