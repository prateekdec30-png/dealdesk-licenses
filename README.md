# DealDesk license feed

This repo holds nothing but subscription license keys, their plan, their expiry
date, and whether they're active or revoked. No app code and no customer names
live here — it's deliberately public so any copy of DealDesk, anywhere, can
check its own license key against `licenses.json` without needing to sign in
to anything.

Each DealDesk install checks this file when it opens (and every few hours
while it stays open). If a key is missing, expired, or marked `"revoked"`,
that copy locks itself with a renewal screen until a valid key is entered.

## Format

```json
{
  "keys": {
    "AB12-CD34-EF56": { "plan": "3month", "expiry": "2027-02-01", "status": "active" }
  }
}
```

- `plan`: one of `1month`, `3month`, `6month`, `yearly` — informational only.
- `expiry`: `YYYY-MM-DD`. The key stops working the day after this date.
- `status`: `"active"` or `"revoked"`. Set to `"revoked"` to cut off a key
  immediately, before its expiry date, without touching anything else.
