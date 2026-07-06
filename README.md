# Bay Area Electronic Events Calendar

A curated, auto-updating calendar of techno, house, EDM, amapiano, afrobeats, and drum & bass events in San Francisco, Oakland, and San Jose. Every event is verified against a live venue, promoter, or ticketing page before it's added. Refreshed by a daily research job.

## 📅 Subscribe

Feed URL:

```
https://raw.githubusercontent.com/cameronking4/bay-events/main/calendar.ics
```

- **Google Calendar:** Settings → *Add calendar* → *From URL* → paste the URL. (Google refreshes subscribed feeds every ~12–24 h.)
- **Apple Calendar (Mac):** File → *New Calendar Subscription…* → paste the URL → set auto-refresh to "Every day".
- **iPhone:** Settings → Calendar → Accounts → Add Account → Other → *Add Subscribed Calendar*.

Or browse [CALENDAR.md](CALENDAR.md) for the human-readable listing.

## How it works

- `events.json` — source of truth (one entry per event, stable UIDs)
- `scripts/build.py` — generates `calendar.ics` (RFC 5545) and `CALENDAR.md`
- A daily scheduled Claude Code job researches new events (19hz.info, RA, venue calendars, Eventbrite/Tixr), verifies them against primary sources, merges them into `events.json`, rebuilds, and pushes — which updates all subscribers.

Tentative events are marked TENTATIVE, cancellations stay in the feed as CANCELLED (so they update rather than silently vanish from your calendar), and approximate start times are flagged in the event description.
