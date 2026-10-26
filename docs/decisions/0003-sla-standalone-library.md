# 0003. Build the SLA engine as a standalone library on built-in .NET types

- **Status:** Accepted
- **Date:** 2026-10-26

## Context
SLA calculation is pure logic with many edge cases. It will be used by the web app, but doesn't need the web app or a database to work.

## Decision
Build `Helpdesk.Sla` as a class library with no dependencies on other projects. Use built-in .NET date and time types (`DateTimeOffset`, `DateOnly`, `TimeOnly`, `TimeZoneInfo`, `TimeProvider`). NodaTime was considered and not used, so the date maths is written and tested by hand.

## Consequences
- Fast, isolated unit tests
- Reusable outside this project
- More hand-written date code to get right, and more tests needed
