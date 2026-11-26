# Atomic Computing — build task (AI Software Engineering Internship)

## Status
- Quiz PASSED. Mike Kasher mailed Mon 23 Nov 2026, 20:14 UTC / Tue 24 Nov 01:44 IST.
- Build task: Trello-style project management tool.
- **Due: within 7 days of the mail → ~Mon 30 Nov 2026. Aim to submit by Sun 29 Nov.**

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
- Pages/views: board switcher (2–3 boards), list add/rename, card add/edit (title, description, due date, labels), search/filter, summary panel.
- Polish bar (his quality rule): must be verified end-to-end before submitting — drag across lists, reload persistence, summary updates live.

## Submit (all three, same email mingwsumit@gmail.com)
- Public GitHub repo (github.com/sumitagg24 — needs your GitHub sign-in; this is the one step still pending)
- Live URL (Vercel free)
- Loom video, max 5 minutes, "record it the way you would show up to a client call"
- Form: https://docs.google.com/forms/d/e/1FAIpQLScSbfBDyyFUZGdntU5GQlKPZlbnErsA8jRfV-cdpzTk8vAb0A/viewform

## Loom script (5 min, client-call style) — draft for him to record
1. (0:00–0:30) Intro: who he is, what the app is — a Trello-style board manager with drag-and-drop, saved data and a client-side board summary.
2. (0:30–2:00) Demo: create a board/list/card, drag a card between lists, reload the page to show data persisted.
3. (2:00–3:30) Board summary (the bonus feature): show the summary panel on a board with overdue/unassigned cards; explain the rules it uses and that it runs client-side with no paid service or API key. Call it a board summary, not AI — there is no model behind it.
4. (3:30–4:30) Code walkthrough: state shape (boards → lists → cards), drag handlers, localStorage sync — all inline in the single `index.html`, briefly.
5. (4:30–5:00) What he'd improve: backend sync + real auth, role-based access as the next bonus, LLM-backed summaries with a key.

## Only he can do
- Record the Loom (facecam, your voice, client-call manner). No tool can record it for you.
- GitHub sign-in if the push needs it; Vercel deploy if it asks for his login.

## Source
- Mike Kasher mail, 23 Nov 2026 20:14 UTC, mingwsumit@gmail.com inbox, subject "Atomic Computing internship: your build task".
