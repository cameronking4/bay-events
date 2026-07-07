# bay-events

Living calendar of Bay Area electronic music events (techno, house, EDM, amapiano, afrobeats, drum & bass) in SF / Oakland / San Jose. Cameron subscribes to the published `calendar.ics`, so correctness matters more than volume: a fake or wrongly-dated event ends up on his phone.

## Files

- `events.json` — single source of truth. Edit only this.
- `scripts/build.py` — generates `calendar.ics` + `CALENDAR.md` from events.json. Validates dupes/dates.
- `calendar.ics`, `CALENDAR.md` — generated; never hand-edit.
- `prompts/daily-research.md` — the prompt the scheduled daily job runs.

## Update workflow (used by the daily job and manual sessions)

1. Research new events for the window **today → +3 months**. Primary sources, in order of usefulness:
   - https://19hz.info/eventlisting_BayArea.php (canonical Bay listing — check this first; it catches warehouse/amapiano/boat events that announce 2–6 weeks out)
   - Venue calendars: 1015.com, publicsf.com/calendar, m.audiosf.com/events, tixr.com/groups/midwaysf (403s — reach via 19hz links or web search), crybaby.live/events, feightsf.com/new-events, thegreatnorthernsf.com, thenewparish.com
   - ra.co/events/us/sanfrancisco, edmtrain.com/san-francisco + /san-jose-ca, Eventbrite SF/Oakland EDM + afrobeats categories
2. **Verification bar:** an event needs a live primary source (venue site, promoter, or ticketing page) showing an explicit date in the correct year. One secondary source only → `"status": "likely"`. Never add from memory or from SEO placeholder pages (VividSeats/TicketSmarter "2026 dates" pages are not confirmations).
3. **Merge rules:**
   - Dedupe by (title, date, venue) — check existing ids before adding. Ids are stable slugs: `artist-venue-YYYYMMDD`. Never change an existing id (it's the calendar UID; changing it duplicates the event in subscribers' calendars).
   - Event moved/changed → update fields in place, same id.
   - Event cancelled → set `"status": "cancelled"` (renders as CANCELLED); don't delete. Use `"status": "removed"` only for events added by mistake.
   - Unknown start time → use venue default and set `"approx": true` (1015: 22:00, Audio night: 21:30, Public Works: 21:30, Midway night: 21:00, Crybaby: 22:00, day parties: 14:00–20:00).
   - `end` earlier than `start` means it crosses midnight — that's handled.
   - Genres from: techno, house, edm, amapiano, afrobeats, dnb, day-party, boat, festival.
4. Re-verify soon-upcoming `likely` and TBA-venue events; also spot-check that next-14-days events haven't been cancelled.
5. Build & publish:
   ```
   python3 scripts/build.py
   git add -A && git commit -m "events: <summary>" && git push
   ```
   The push is what updates subscribers — never skip it after changing events.json.

## Standing leads to re-check (as of 2026-07-07)

- Sunset Sound System summer boat party — not announced yet (only the Oct 25 Halloween boat, already tracked); watch sunsetsoundsystem.com/events
- Second Sky (Porter Robinson) — no 2026 edition announced; watch secondskyfest.com
- Afro Rave (Oakland) — no longer at The New Parish; 2026 editions were at Hella Bees and Starline Social Club. Watch the Afrobeats Oakland Eventbrite organizer, not thenewparish.com
- Bissap Baobab amapiano nights — site calendar is stale; they announce on short lead via Eventbrite/Instagram
- Mura Masa // Curve 2026-07-18 (tracked, likely) — venue still TBA; Jungle Soundclash 2026-08-22 (tracked, likely) — vanished from 19hz, may be pulled
- Oakland warehouse parties via 19hz; Outside Lands night-show additions; Halcyon Sep–Oct listings not yet published
