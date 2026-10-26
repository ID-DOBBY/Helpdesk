# SLA Engine — Plan (v0.1)

Part of the Helpdesk portfolio project. The SLA engine is a standalone C# library that answers two questions about a ticket:

1. **When is it due?**
2. **Is it on track, at risk, breached, or met?**

It has no UI and no database: data goes in, an answer comes out.

---

## 1. Definition of done (v0.1)

- [ ] All tasks in section 6 are complete
- [ ] All tests pass in GitHub Actions (CI)
- [ ] The README explains what it does, shows a usage example, and lists the key design decisions
- [ ] Tagged `v0.1` on GitHub

---

## 2. Tech stack

| Area | Choice | Why |
|---|---|---|
| Language | **C#** | The language you already know; used for the whole helpdesk |
| Runtime | **.NET 10** (LTS) | Current long-term support release |
| Project type | **Class library** (`Helpdesk.Sla`) | Pure logic, reusable by the web app later |
| Dates & times | **Built-in .NET types**: `DateTimeOffset`, `DateOnly`, `TimeOnly`, `TimeSpan`, `TimeZoneInfo` | No extra dependency; time zone id `Europe/Malta` |
| "Now" in tests | **`TimeProvider`** (built into .NET) + **`FakeTimeProvider`** (`Microsoft.Extensions.TimeProvider.Testing`) | Tests control the clock instead of depending on the real time |
| Config | **`System.Text.Json`** | Load SLA policies and settings from a JSON file |
| Testing | **xUnit** | Standard .NET test framework |
| Assertions | **xUnit `Assert`** (or **Shouldly** if you want more readable asserts) | Free and simple |
| Coverage | **coverlet** (included in the xUnit template) | Show test coverage in CI |
| CI | **GitHub Actions** with `actions/setup-dotnet` | Build and test on every push; badge for the README |
| IDE | **Visual Studio 2026 Community** or **JetBrains Rider** (free for non-commercial use) | Either works |
| Version control | **Git + GitHub** | Issues for tasks, one commit per task |

**Considered and not used:** NodaTime (an excellent date/time library). This was left out on purpose so the date maths is written by hand. Note this in the README as a design decision.

**Stretch:** Stryker.NET (mutation testing), which checks whether your tests actually catch bugs.

### Later in the full helpdesk (not needed now)

| Area | Choice |
|---|---|
| Web API | ASP.NET Core |
| UI | Blazor |
| Database | PostgreSQL via EF Core (Npgsql provider) |
| Login & roles | ASP.NET Core Identity |
| Running locally | Docker Compose |
| Integration tests | Testcontainers |

---

## 3. Scope

### In v0.1
- One fixed schedule (e.g. Mon–Fri, 08:00–17:00)
- Two timers per ticket:
  - **Response:** time to first reply
  - **Resolution:** time to resolve
- Targets per priority, counted in working hours (e.g. High = respond in 2h, resolve in 8h)
- Pausing on statuses listed in config (e.g. *Waiting on customer*). Pauses apply to the **resolution** timer only.
- Holidays calculated by rules:
  - Fixed dates (e.g. 1 Jan, 8 Sep, 25 Dec)
  - Easter-based dates (e.g. Good Friday = Easter − 2 days)
- Times stored in **UTC** and converted to **Malta time** for the business-hours maths

### Not in v0.1 (goes in `IDEAS.md`)
- Different hours per weekday
- Per-team calendars
- Moving a holiday that falls on a weekend to a weekday
- Multiple time zones

---

## 4. Requirements as examples (these become tests)

Assume Mon–Fri, 08:00–17:00.

| # | Situation | Expected |
|---|---|---|
| 1 | Opened Tue 10:00, 8h target | Due **Wed 09:00** |
| 2 | Opened Tue 07:00 (before opening), 1h | Due **Tue 09:00** |
| 3 | Opened Tue 17:00 exactly, 1h | Due **Wed 09:00** |
| 4 | Opened Sat 11:00, 2h | Due **Mon 10:00** |
| 5 | Opened Fri 15:00, 8h, Monday is a holiday | Due **Tue 14:00** |
| 6 | Good Friday 2026 | **3 April 2026** is a holiday (Easter = 5 April) |
| 7 | Paused Wed 09:00 → Thu 12:00 | That time doesn't count |
| 8 | First reply after 1h50 with a 2h response target | Response timer = **Met** |
| 9 | 75% or more of the time used, not yet due | **At risk** |
| 10 | Past due and not resolved | **Breached** |

---

## 5. Design sketch

```
EasterCalculator      → Easter Sunday for any year
IHolidayRule          → FixedDateHoliday, EasterOffsetHoliday
WorkingSchedule       → start time, end time, workdays
BusinessCalendar      → IsWorkingTime(t)
                        WorkingTimeBetween(a, b)
                        AddWorkingTime(start, duration)
SlaPolicy             → priority, response target, resolution target
SlaSettings           → pause statuses, at-risk threshold (75%)
TicketTimeline        → opened at, status changes, first reply at
SlaEvaluator          → Evaluate(timeline, policy, now) → SlaResult
SlaResult             → per timer: Due, Elapsed, Remaining, State
```

### Solution layout

```
Helpdesk.sln
├── src/
│   └── Helpdesk.Sla/
├── tests/
│   └── Helpdesk.Sla.Tests/
├── docs/
│   └── PLAN.md
├── .github/workflows/ci.yml
├── IDEAS.md
└── README.md
```

---

## 6. Tasks

Each task should take about one sitting and ends with a commit. Make each one a GitHub Issue.

### Setup
- [ ] **1.** Create the repo, solution, `Helpdesk.Sla` library and `Helpdesk.Sla.Tests` xUnit project. Add `.gitignore` and stub `README.md` / `IDEAS.md`. Push.
- [ ] **2.** GitHub Actions workflow: restore, build, test on every push. Add the status badge to the README.

### Holidays
- [ ] **3.** `EasterCalculator` + tests (Easter 2025 = 20 Apr, 2026 = 5 Apr, 2027 = 28 Mar)
- [ ] **4.** `IHolidayRule`, `FixedDateHoliday`, `EasterOffsetHoliday`, plus a Malta rule set (test #6)

### Calendar
- [ ] **5.** `WorkingSchedule` + `IsWorkingTime`
- [ ] **6.** `WorkingTimeBetween(a, b)`
- [ ] **7.** `AddWorkingTime(start, duration)` (tests #1–5)
- [ ] **8.** UTC ↔ Malta time conversion tests (including across a daylight-saving change)

### SLA
- [ ] **9.** `SlaPolicy` + `SlaSettings`, loaded from JSON
- [ ] **10.** Response timer (test #8)
- [ ] **11.** Resolution timer with pausing (test #7)
- [ ] **12.** States: On track / At risk / Breached / Met (tests #9–10)

### Finish
- [ ] **13.** README: what it does, usage example, design decisions. Tag `v0.1`.

---

## 7. Working rules

- **One task at a time.** Don't open the next task until the current one is committed.
- **Write the test first** using the table in section 4, then make it pass.
- **New idea mid-task?** Write it in `IDEAS.md` and get back to the task.
- **Stuck for more than 30 minutes?** Ask for a hint, not code.
