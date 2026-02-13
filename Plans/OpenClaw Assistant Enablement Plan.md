# OpenClaw Assistant Enablement Plan

## Goal
Get Jarvis fully operational for calendar and email management with reliable remote administration.

## Current State (as of 2026-02-13)
- ✅ OpenClaw gateway running on Mac mini
- ✅ Telegram channel connected
- ✅ Core CLIs installed (`gog`, `himalaya`, `remindctl`, `memo`, `imsg`)
- ✅ Apple Reminders access granted
- ✅ Tailscale already set up
- ⚠️ Google OAuth token currently invalid (`invalid_grant`)
- ⚠️ `himalaya` email config not yet set up
- ⚠️ No cron automations configured yet

## Phase 1 — Re-enable Google Workspace access (priority)
1. On Mac mini (in-person GUI session), run:
   ```bash
   gog auth add matthewsavich@gmail.com --services gmail,calendar
   ```
2. Complete browser consent flow.
3. Verify token works:
   ```bash
   gog calendar events primary --from "$(date -u +%Y-%m-%dT%H:%M:%SZ)" --to "$(date -u -v+1d +%Y-%m-%dT%H:%M:%SZ)"
   ```
4. Ask Jarvis to confirm live read access by listing this week’s events.

## Phase 2 — Email capability choice

### Option A (recommended initially): Gmail via `gog`
- Use `gog` for inbox search, triage, and draft workflows.
- Skip `himalaya` unless non-Google accounts are needed.

### Option B: Add `himalaya` for multi-account email
1. Configure account(s):
   ```bash
   himalaya account configure
   ```
2. Validate read/send capability.
3. Add account aliases and default behavior notes in TOOLS.md.

## Phase 3 — Automations to enable
Once Google auth is fixed, create these automations:

1. **Weekday 08:00** — Morning Brief
   - Today’s calendar
   - Priority unread emails
   - Immediate action items

2. **Weekday 13:00** — Midday Check
   - Next meetings in next 4 hours
   - New urgent emails

3. **Weekday 17:30** — End-of-day Wrap
   - Follow-up reminders
   - Tomorrow’s first commitments

## Phase 4 — Operating workflow
- Ask Jarvis in Telegram for ad-hoc tasks:
  - “What’s next on my calendar?”
  - “Summarize urgent unread emails.”
  - “Draft a reply to X.”
  - “Set a reminder for Y at Z time.”
- Keep “send externally” actions approval-gated where desired.

## Guardrails
- No secrets/tokens in notes or commits.
- Keep external sends explicit (unless pre-approved rule exists).
- Review weekly whether automations are useful vs noisy.

## Success Criteria
- Calendar read + event management works from chat
- Email triage + draft generation works from chat
- 3 scheduled daily check-ins running reliably
- Remote maintenance possible via Tailscale + Screen Sharing when needed

## Quick Command Reference
```bash
# Google auth (fix)
gog auth add matthewsavich@gmail.com --services gmail,calendar

# Check auth accounts
gog auth list

# Calendar sample read
gog calendar events primary --from <iso> --to <iso>

# Optional non-Google email setup
himalaya account configure
```
