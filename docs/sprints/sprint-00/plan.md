# Sprint 00 — Plan (Setup)

**Dates:** YYYY-MM-DD → YYYY-MM-DD (1 week)
**Sprint goal:** The repository, process and backlog are ready, so Sprint 1 can start coding on day one.

## Checklist

### Repository
- [ ] Create the GitHub repo (public, MIT license)
- [ ] Add these docs, `README.md`, `CONTRIBUTING.md`, `CHANGELOG.md`
- [ ] Run `dotnet new gitignore`
- [ ] Create the solution, `src/Helpdesk.Sla` (classlib) and `tests/Helpdesk.Sla.Tests` (xUnit) — **TECH-1**
- [ ] Add a GitHub Actions workflow: restore, build, test on push and PR — **TECH-2**

### GitHub setup
- [ ] Labels: `story`, `bug`, `tech-debt`, `spike`, `docs`, `sla-engine`, `rules-engine`, `web`, `infra`
- [ ] Projects board with columns: Backlog, Sprint, In progress, In review, Done
- [ ] Milestones: `Sprint 01`, `Sprint 02`
- [ ] Branch protection on `main`: require a PR and passing CI before merging

### Backlog
- [ ] Create an issue for each story in `docs/requirements/sla-engine.md` (SLA-1 to SLA-8)
- [ ] Order the backlog
- [ ] Write `docs/sprints/sprint-01/plan.md`

## Done when
Sprint 1 can start with a green CI badge, an ordered backlog and a sprint plan.
