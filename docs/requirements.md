# SupportDesk AI — Requirements (MVP)

## Problem
Customer support runs through a shared inbox. Tickets get lost, two agents
sometimes answer the same customer, urgent issues are not visible, and the
owner has no idea what customers complain about most.

## Context
- Team: 1 owner (Dana), 3 support agents (incl. Maria, off on Fridays)
- Volume: ~50 tickets/day, expected spike after the February launch
- Target: first version live by mid-January

## Users & Roles
| Role     | Can do |
|----------|--------|
| Customer | Create tickets, comment, view own tickets, reopen within 7 days |
| Agent    | View all tickets, assign to self, change status/priority, comment |
| Admin    | Everything an agent can + manage team members + view dashboard |

## Ticket Lifecycle
- Statuses: Open → In Progress → Waiting on Customer → Resolved → Closed
- Priorities: Low, Medium, High, Urgent
- Categories (set by AI, editable by agents): Billing, Technical, Account, Feature Request, Other

## User Stories

1. As a customer, I want to submit a ticket through a web form so that my problem is tracked.
   - AC: title and description are required
   - AC: the ticket is created with status "Open"
   - AC: I can see my ticket in "My Tickets" right after submitting

2. As a customer, I want the system to understand my issue automatically so that it reaches the right person faster.
   - AC: on creation, AI sets category, priority and a one-line summary
   - AC: if the AI call fails, the ticket is still created with priority "Medium" and category "Other"

3. As an agent, I want to assign a ticket to myself so that no one else replies to the same customer.
   - AC: a ticket has at most one assignee
   - AC: other agents see who owns the ticket
   - AC: an agent cannot take a ticket already assigned to someone else (only an admin can reassign)

4. As an agent, I want to filter and sort tickets by status, priority and category so that I handle urgent issues first.
   - AC: filtering and pagination happen on the server
   - AC: default sort is priority (Urgent first), then oldest first

5. As an agent, I want to change a ticket's status and add comments so that the customer and the team know the progress.
   - AC: every status change and comment is saved with the author and time
   - AC: the customer sees agent comments on their ticket

6. As a customer, I want to reopen a resolved ticket within 7 days so that a returning problem keeps its history.
   - AC: "Reopen" is available only for 7 days after the ticket is resolved
   - AC: after 7 days, the customer must create a new ticket

7. As an admin, I want to add and deactivate agents so that I can manage the team without a developer.
   - AC: deactivated agents cannot log in, but their ticket history stays

8. As an admin, I want a dashboard with ticket counts by status, priority and category so that I know what customers complain about most.
   - AC: counts are shown for the last 7 and 30 days

## Out of Scope (v2)
- Email integration (create/reply to tickets by email, migrate old emails)
- SMS alerts, VIP routing
- Company accounts (customers of the same company see each other's tickets)
- Attachments
- Auto-close for "Waiting on Customer" tickets, SLA, business hours
- Saved replies, weekly email reports
- Merging duplicates, spam filtering, multiple languages
- Data retention and GDPR handling for payment details

## Open Questions
- Build vs buy: why not Zendesk/Freshdesk?
  → Decision: custom build for AI triage and tight integration with our product.
- What does "urgent within an hour" mean outside business hours and on weekends?
- Who triages tickets on Fridays when Maria is off?

## Success Metrics
- % of tickets with a first response on the same day
- % of Urgent tickets answered within 1 hour (business hours)
- No ticket answered by two agents
