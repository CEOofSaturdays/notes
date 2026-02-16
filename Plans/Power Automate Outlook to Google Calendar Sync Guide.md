# Power Automate Outlook → Google Calendar Sync Guide

## Goal
Reliable one-way sync from Work Outlook calendar (source of truth) to Google Calendar.

## Architecture
- Source: Microsoft 365 Outlook work calendar
- Destination: Google Calendar (`Work Calendar` or `Work Sync`)
- Direction: One-way (Outlook → Google)
- Behaviors: create, update, delete/cancel

## Before You Build
1. Confirm destination Google calendar.
2. Keep old ICS import running temporarily during testing.
3. Decide privacy mode:
   - Full details, or
   - Busy-only for sensitive events.

## Build 3 Power Automate Flows

### Flow A — Create
**Trigger**
- Office 365 Outlook: `When an event is added, updated or deleted (V3)`
- Change type: Created

**Actions**
1. Optional condition to skip private/no-sync events.
2. Google Calendar: `Create an event`.
3. Include marker in description:
   - `Source: Outlook`
   - `OutlookEventId: <id or iCalUId>`

### Flow B — Update
**Trigger**
- Same trigger
- Change type: Updated

**Actions**
1. Find matching Google event via mapping key.
2. If found: `Update event`.
3. If not found: create event (self-heal).

### Flow C — Delete/Cancel
**Trigger**
- Same trigger
- Change type: Deleted (or cancelled)

**Actions**
1. Find mapped Google event.
2. Delete/cancel in Google.

## Mapping (Critical)
Use a stable link between Outlook and Google events:
- Store `OutlookEventId` in Google description/extended property, and/or
- Keep a mapping table (SharePoint/Dataverse):
  - OutlookEventId
  - GoogleEventId
  - LastSyncTime
  - Status

## Migration Plan (from ICS)

### Phase 1 — Shadow test (1–2 days)
- Create `Work Sync (PA Test)` calendar in Google.
- Point flows to test calendar.
- Validate create/update/delete behavior.

### Phase 2 — Cutover
1. Disable/remove old ICS import.
2. Point flows to production Google work calendar.
3. Keep test calendar for rollback for 24h.

### Phase 3 — Cleanup
- Remove duplicate ICS-origin events.
- Keep Power Automate events (marker helps identify).

## Guardrails
- Ignore all-day OOO events if not needed.
- Ignore tentative events if desired.
- Support `#nosync` keyword/category skip.
- Add retries and failure alerts (Teams/email).

## Recommended Field Mapping
- Subject → Title
- Start/End → Start/End
- Location → Location
- Body (trimmed) → Description
- Private events → title `Busy` + redacted details

## Notes
- Keep timezone fixed to `Australia/Perth`.
- One-way sync avoids loops and duplicate churn.
