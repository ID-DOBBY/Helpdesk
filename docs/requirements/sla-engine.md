# Requirements — SLA Engine (Epic)

Business hours for all examples: **Mon–Fri, 08:00–17:00, Europe/Malta**.

## Stories

### SLA-1 · Public holidays
**As an** admin, **I want** public holidays excluded from SLA time **so that** tickets aren't due on days off.
- [ ] Easter Sunday is calculated correctly (2025-04-20, 2026-04-05, 2027-03-28)
- [ ] Fixed-date holidays are supported (e.g. 1 Jan, 25 Dec)
- [ ] Easter-relative holidays are supported (Good Friday 2026 = 2026-04-03)
- [ ] A Malta holiday rule set is provided

### SLA-2 · Business hours
**As an** admin, **I want** SLA time counted only during working hours **so that** deadlines are realistic.
- [ ] Time outside 08:00–17:00, on weekends or on holidays is not working time
- [ ] Working time between any two moments can be calculated

### SLA-3 · Due date calculation
**As an** agent, **I want** to know exactly when a ticket is due **so that** I can prioritise.
- [ ] Opened Tue 10:00 + 8h → due Wed 09:00
- [ ] Opened Tue 07:00 + 1h → due Tue 09:00
- [ ] Opened Tue 17:00 + 1h → due Wed 09:00
- [ ] Opened Sat 11:00 + 2h → due Mon 10:00
- [ ] Opened Fri 15:00 + 8h, Monday a holiday → due Tue 14:00

### SLA-4 · Time zones
**As a** developer, **I want** times stored in UTC and calculated in Malta time **so that** results are correct across daylight-saving changes.
- [ ] All inputs and outputs are UTC
- [ ] Working-time calculations across a DST change give the correct result

### SLA-5 · SLA policies
**As an** admin, **I want** response and resolution targets per priority, loaded from config, **so that** I can change them without code changes.
- [ ] Policies load from JSON
- [ ] Invalid config gives a clear error

### SLA-6 · Response timer
**As a** team lead, **I want** to track time to first reply **so that** customers aren't left waiting.
- [ ] First reply after 1h50 with a 2h target → **Met**
- [ ] No reply and past the target → **Breached**

### SLA-7 · Resolution timer with pausing
**As an** agent, **I want** the clock to stop while waiting on the customer **so that** I'm not penalised for their delay.
- [ ] The statuses that pause the clock are configurable
- [ ] Paused Wed 09:00 → Thu 12:00: that time doesn't count
- [ ] Pausing does not affect the response timer

### SLA-8 · SLA states
**As an** agent, **I want** a clear state on each timer **so that** I can see problems at a glance.
- [ ] ≥ 75% of the time used, not yet due → **At risk** (threshold configurable)
- [ ] Past due and not complete → **Breached**
- [ ] Completed in time → **Met**
- [ ] Otherwise → **On track**

## Technical
- **TECH-1** · Repository, solution and test project setup
- **TECH-2** · CI: build and test on every push and pull request
