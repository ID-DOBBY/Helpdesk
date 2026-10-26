# Product Vision

## Problem
Small IT support teams often run on shared inboxes or basic ticket tools. Deadlines are tracked by gut feeling, tickets get assigned by hand, and when something goes wrong nobody can reconstruct exactly what happened to a ticket and when.

## Users
| User | Needs |
|---|---|
| **Requester** | Log an issue easily and see its progress |
| **Agent** | Know what to work on next and how long they have |
| **Team lead / Admin** | Route tickets automatically, see SLA performance, audit history |

## Product goal
A helpdesk where **routing is set by rules**, **SLAs follow real business hours**, and **any ticket's full history can be rebuilt at any point in time**.

## Goals
1. Deadlines that respect working hours, holidays and paused tickets
2. Automatic routing set by admin-written rules, not code changes
3. A complete, trustworthy audit trail for every ticket

## Non-goals
- Live chat, phone or telephony integration
- Billing or invoicing
- Multi-tenant SaaS hosting
- A mobile app

## Success measures
- SLA engine and rules engine are fully unit-tested and pass CI
- An agent can see "due in X" and the SLA state on every ticket
- A new ticket is routed automatically by at least one admin-written rule
