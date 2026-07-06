You are running the daily update for the bay-events calendar project (Bay Area electronic music events). Work in this directory (~/bay-events).

Read CLAUDE.md and follow its update workflow exactly. Summary of the job:

1. `git pull` first.
2. Research NEW or CHANGED electronic music events (techno, house, EDM, amapiano, afrobeats, drum & bass) in SF / Oakland / San Jose / greater Bay Area for the window today through +3 months. Check, at minimum: 19hz.info/eventlisting_BayArea.php, ra.co/events/us/sanfrancisco, edmtrain.com/san-francisco and /san-jose-ca, and the venue calendars listed in CLAUDE.md. Also re-check the "standing leads" section of CLAUDE.md.
3. Verify every candidate against a live primary source (venue/promoter/ticketing page showing an explicit date in the correct year) before adding. Single secondary source → status "likely". No source → don't add.
4. Merge into events.json per CLAUDE.md rules: dedupe against existing ids by (title, date, venue); stable ids (artist-venue-YYYYMMDD); update changed events in place; mark cancellations status "cancelled"; re-verify "likely" and TBA events happening within 14 days.
5. Run `python3 scripts/build.py` — it must print OK.
6. If events.json changed: `git add -A && git commit -m "events: <short summary of adds/changes>" && git push`. If nothing changed, do nothing (no empty commits).

Keep total additions honest — it is fine to add zero events on a quiet day. Never invent events, never trust SEO ticket-resale placeholder pages, and never change an existing event's id.
