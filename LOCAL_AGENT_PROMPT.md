PROMPT FOR LOCAL AI AGENT — Atomic Computing build task (Trello-style board app)

Context: This folder is my submission project for the Atomic Computing AI Software Engineering Internship build task (from Mike Kasher). The app already exists and works — index.html is a complete single-file static app: Trello-style boards, lists and cards, drag-and-drop between lists, data saved in localStorage, and a client-side AI board summary panel. It has 3 boards and 23 cards of seed data. It was already polished once (deep-ocean gradient, frosted glass, light + dark mode).

Your job: take this working app and make it submission-ready. Do NOT rewrite it from scratch — read index.html fully first, then improve it in place.

1. VERIFY DRAG-AND-DROP FIRST (most important)
- Open the app in a real browser and drag a card from one list to another using real mouse events. Confirm the card moves AND the move survives a page reload (localStorage).
- If drag is broken, fix it. Keep the card editor's "List" dropdown as a second way to move cards — never remove that fallback.
- Test on both desktop and a narrow mobile viewport.

2. POLISH THE FRONTEND FURTHER
- Tighten spacing, alignment and typography; make hover, focus and active states consistent everywhere.
- Smooth micro-interactions: card pick-up/landing states while dragging, subtle list highlight on drag-over, animated modal open/close.
- Make it fully responsive: boards must scroll horizontally on small screens, cards must stay readable, modals must fit a phone screen.
- Improve empty states (empty list, empty board, no search results) with clear text and a call to action.
- Check contrast and keyboard accessibility: Tab order, Esc closes modals, visible focus rings. Keep light + dark mode both looking clean.

3. ADD THESE FEATURES (only if not already present; improve them if they are)
- Due dates on cards, with overdue (red) and due-soon (amber) badges, and a filter for overdue cards.
- Checklists inside cards with a progress bar (e.g. 2/5 done).
- Archive cards, with an archived view and restore.
- Activity log per board (card created / moved / edited, with time).
- Duplicate a board, and 2 starter board templates (e.g. "Product launch", "Study plan").
- Export a board as JSON and import it back.
- Keyboard shortcuts: N = new card, / = search, Esc = close.
- Drag cards between boards, not just between lists.
- Assignee field on cards (just a name, no accounts).
- Card count on each list header.
- Undo when a card/list is deleted (toast with Undo, 5 seconds).

4. HARD RULES
- No backend, no database, no paid service, no API key required. Everything still runs as a static site from localStorage.
- Keep the existing 3 boards and 23 cards of seed data; only add demo content where a new feature needs it.
- Keep the AI board summary client-side (counts, overdue/due-soon, busiest list, suggested next action) — no fake AI claims, no invented API.
- Keep it deployable as a static site with no build step (single index.html, or index.html + styles.css + app.js — Vercel static, no framework needed).
- Do not break anything that already works. Do not submit anything or create any accounts.

5. VERIFY END-TO-END BEFORE YOU FINISH
Run through this checklist in a real browser and fix anything that fails:
- Create a board, list and card; edit and delete a card; drag a card between lists AND between boards; reload — everything persists.
- Search and label filters return the right cards.
- AI summary updates when cards change.
- Due-date badges, checklists, archive/restore, export/import, undo toast all work.
- No console errors on load or during any of the above.

6. DELIVERABLES
- The updated project files in this same folder.
- A CHANGELOG.md listing exactly what you changed, added and fixed.
- A short "NEXT STEPS FOR ME" note at the end of CHANGELOG.md: 1) push this folder to a new PUBLIC GitHub repo, 2) deploy it free on Vercel (static, no build command), 3) record a Loom video under 5 minutes showing a drag, a reload, and the AI summary, 4) submit the GitHub link + live URL + Loom link at https://docs.google.com/forms/d/e/1FAIpQLScSbfBDyyFUZGdntU5GQlKPZlbnErsA8jRfV-cdpzTk8vAb0A/viewform (deadline Mon 30 Nov 2026, aim Sun 29 Nov).
