# 0002. Use GitHub Flow for branching

- **Status:** Accepted
- **Date:** 2026-10-26

## Context
A branching model is needed. Long-lived per-component branches (e.g. `sla-main`, `sla-staging`) and GitFlow were considered.

## Decision
Use GitHub Flow: `main` is always releasable, work happens on short-lived branches (one per issue) merged through pull requests with passing CI. Releases are marked with tags.

## Consequences
- `main` always builds and passes tests
- No long-lived branches drifting apart
- Staging environments, if needed later, are handled by the deploy pipeline rather than by branches
