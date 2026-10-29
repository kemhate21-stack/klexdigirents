# KlexDigirents: rebuilt site

A single-file static site (`index.html`). It needs no build step, server or API key, so it runs on GitHub Pages as-is.

## What's new vs. the old site

- **KlexBot (RAG chat agent):** runs entirely in the browser. It retrieves answers from the FAQ knowledge base (`KB` in the script) using BM25 search with Taglish synonyms. It also has two tools:
  - **Availability lookup:** understands questions like "avail ba C813 bukas?", "this Saturday", "nov 8-10 c533" or "11/8". It checks them against the schedule and suggests other cameras or the next open date.
  - **Price calculator:** for questions like "magkano 3 days?".
- **Booking availability:** a calendar for all cameras or for one camera. Tap a pickup day, then a return day. The date checker shows which cameras are free and a cost estimate.
- **FAQ:** a searchable FAQ with category filters. It shares the same knowledge base as the bot, so editing one updates both.
- **Owner panel removed:** it had a password visible in the page source and only saved to the owner's own browser.
- Renter names and phone numbers are no longer shown publicly.

## Making availability real (important)

The old site saved bookings in each visitor's own browser (`localStorage`), so visitors only ever saw demo data. Pick one of these:

1. **Google Sheet (recommended):** make a tab with the columns `camera,start,end,status`, for example `C613,2026-11-03,2026-11-04,confirmed`. Then go to File → Share → Publish to web, choose that tab as **CSV**, and paste the link into `CONFIG.bookingsCsvUrl`. After that, updating the sheet updates the site. The page re-checks every 5 minutes.
2. **Manual:** add entries to `MANUAL_BOOKINGS` in `index.html` and push.

## Editing
- Prices, form URL and Messenger link: the `CONFIG` object at the top of the `<script>`.
- FAQ and bot answers: the `KB` array. Add `tags` with words people actually type, Tagalog included.
- Camera info: the `CAMERAS` object.
