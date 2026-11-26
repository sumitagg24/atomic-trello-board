# Atomic Computing — build task (AI Software Engineering Internship)

## Status
- Quiz PASSED. Mike Kasher mailed Mon 23 Nov 2026, 20:14 UTC / Tue 24 Nov 01:44 IST.
- Build task: Trello-style project management tool.
- **Due: within 7 days of the mail → ~Mon 30 Nov 2026. Aim to submit by Sun 29 Nov.**
- **Ready:** app + public GitHub repo + live Vercel URL. Only the Loom and the form remain.

## What to build (from Mike's mail, verbatim requirements)
- Boards, lists, cards
- Drag-and-drop cards between lists
- Data saved (persisted — localStorage is fine for a prototype; say so in the video)
- ONE bonus feature: **AI board summary** (recommended — fits his AI profile) OR role-based access (owner / member / viewer)
- Deploy on a free host needing no credit card: Netlify, Vercel, GitHub Pages, Cloudflare Pages, Render or Replit. No paid cloud account needed.
- AI coding tools are fine, as long as he can explain the code in the video.

## Build as shipped (this is what is in `index.html`)
- Stack: one self-contained static `index.html` — plain HTML, CSS and vanilla JavaScript, no framework, no build step, no npm install, no backend. It runs by opening the file or serving it from any static host. State in localStorage (seed with a realistic demo board: e.g. "Product Launch" with Backlog / Doing / Review / Done).
- Drag-and-drop: native HTML5 drag events (dragstart / dragover / drop) — no dependency, precise insert order, cross-board by dropping on a board tab. Touch and keyboard users move a card with the Board / List selectors in its editor.
- Board summary (the brief's "AI board summary" bonus, wrapped as a rules-based panel): client-side, no API key — per-board counts, overdue / due-soon cards, busiest list, suggested next action ("3 cards overdue, 2 unassigned — start with…"). It runs entirely in the browser with no network call, which keeps it demoable with zero paid account and honest in the video.
- Pages/views: board switcher (3 boards), list add/rename, card add/edit (title, description, due date, labels, assignee, checklist), search/filter, archive, activity log, summary panel.
- Polish bar (his quality rule): must be verified end-to-end before submitting — drag across lists, reload persistence, summary updates live.

## Submit (same email mingwsumit@gmail.com)
- Public GitHub repo — **done:** https://github.com/sumitagg24/atomic-trello-board
- Live URL — **done:** https://atomic-trello-board.vercel.app
- Loom video, max 5 minutes, "record it the way you would show up to a client call"
- Form: https://docs.google.com/forms/d/e/1FAIpQLScSbfBDyyFUZGdntU5GQlKPZlbnErsA8jRfV-cdpzTk8vAb0A/viewform

## Loom script (5 min, client-call style) — draft for him to record

Before recording: open **https://atomic-trello-board.vercel.app**, click **Reset demo data** so the board starts clean, and close the console.

1. (0:00–0:30) Intro: who he is, what the app is — a Trello-style board manager with drag-and-drop, saved data and a client-side board summary. Keep the live URL visible in the address bar and say it is deployed on Vercel.
2. (0:30–2:00) Demo: open a board, add a card, then open it and set a due date, two labels, an assignee and one checklist item. Save, drag the card between lists (point at the drop line), then drag a card onto another board's tab to show cross-board moves. Delete a card and hit Undo, or run a quick label/overdue filter if time allows. Reload the page to show the card, order and labels persisted.
3. (2:00–3:30) Board summary (the bonus feature): show the panel on a board with overdue/unassigned cards — totals, completion, overdue, due soon, unassigned, cards per list, busiest list and the suggested next action. Explain that it is computed client-side from the live board with no paid service or API key, and call it a rules-based board summary, not AI — there is no model behind it.
4. (3:30–4:30) Code walkthrough: state shape (boards → lists → cards), `save()` / `load()` with `localStorage`, `render()`, the native drag handlers (`dragstart` / `dragover` / `drop` and `moveCardWithin` / `moveCardToBoard`), and `buildSummaryData()`. All inline in the single `index.html`.
5. (4:30–5:00) What he'd improve next: backend sync + real accounts and role-based access, LLM-backed summaries with a key, and splitting the single file with tests.

### Brief coverage checklist (tick while recording)

- [ ] Live deployed URL visible (0:00–0:30)
- [ ] Boards, lists and cards shown, with a card created/edited (0:30–2:00)
- [ ] Drag between lists with a clear drop indicator (0:30–2:00)
- [ ] Data saved — reload proves it persisted (0:30–2:00)
- [ ] Bonus: live board summary explained (2:00–3:30)
- [ ] Code explained — state, storage, drag, summary (3:30–4:30)
- [ ] Total runtime under 5 minutes

## Only he can do
- Record the Loom (facecam, your voice, client-call manner). No tool can record it for you.
- Submit the form with the repo, live URL and Loom link.

## Source
- Mike Kasher mail, 23 Nov 2026 20:14 UTC, mingwsumit@gmail.com inbox, subject "Atomic Computing internship: your build task".
