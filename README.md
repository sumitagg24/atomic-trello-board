# Atomic Computing — Trello-style board app

Build task for the Atomic Computing AI Software Engineering Internship (Mike Kasher).
Due Mon 30 Nov 2026 — aim to submit Sun 29 Nov.

## What it is

**Atomic Boards**, a Trello-style project board manager: boards, lists and cards, drag and drop
between lists **and between boards**, checklists, due dates, archive, an
activity log, undo, JSON import/export, and a client-side board summary panel
(counts, overdue / due-soon cards, busiest list, suggested next action).

Everything runs in one static `index.html` — no backend, no database, no build
step and no API key required. Data is saved in `localStorage` and reloads with
the page. 3 boards and 23 cards of seed data ship with it.

**Live:** https://atomic-trello-board.vercel.app

## Run it

Just open `index.html` in a browser. Or serve the folder:

```
python3 -m http.server 8000     # Windows: py -m http.server 8000
```

then open http://localhost:8000

## Features

- **Boards, lists, cards** — create, rename, delete (deleting a board or a list
  asks for confirmation); click the board or list title to rename it in place.
- **Drag and drop** — native HTML5 events (`dragstart` / `dragover` / `drop`):
  move cards between lists, reorder inside a list, and drop a card onto a board
  tab to move it to another board. A drop line shows where it will land.
- **Card editor** — title, description, due date, assignee (free-text name with
  suggestions), colour labels (several per card), checklist, and **Board / List**
  selectors that move the card without dragging (keyboard- and touch-friendly
  fallback).
- **Checklists** — add, tick and remove items; the editor and the card face show
  progress (e.g. `2/5`) with a progress bar.
- **Due dates** — red overdue and amber due-soon (within 2 days) badges, plus
  **Overdue** and **Due soon** filters next to the label filters.
- **Search** across card titles, descriptions, assignees, labels and checklist
  text, with a match count and clear empty state.
- **Archive** — archive cards instead of deleting them, then restore or delete
  them permanently from the archived view.
- **Activity log** per board — who/what/when for created, moved, edited,
  archived, restored and deleted items.
- **Undo** — deleting a card or a list shows a toast with **Undo** for 5 seconds.
- **Templates** — Product launch and Study plan, available when creating a board
  or from an empty board.
- **Duplicate board**, **export board as JSON**, **import JSON** back in.
- **Board summary panel** — computed on this device from the live board: totals,
  completion, overdue / due-soon / unassigned counts, cards per list and a
  suggested next action. No API key needed.
- **White-first theme with a black dark mode.** The header has a sun/moon button that switches between the light theme and a black dark theme (neutral greys, no blue cast; only the accent and wordmark carry colour), remembers the choice, and starts from your system preference. Every surface reads the same CSS variables, so both themes cover the whole UI.
- **Responsive** — on phones the board scrolls horizontally with snap points,
  cards stay readable, dialogs fit the screen and the summary opens as a sheet.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `N` | New card in the last-used list |
| `/` | Focus search |
| `Esc` | Close dialog / menu, or clear filters |

Cards are focusable: `Tab` to a card and press `Enter` to open it. Dialogs trap
`Tab` and restore focus when they close.

## Notes

- Dragging uses the browser's native HTML5 drag events, so it works with a
  mouse or trackpad. On a touch device, tap a card and use the **Board** and
  **List** selectors in its editor to move it.
- The summary panel is entirely local: counts, deadlines and the suggested next
  action are computed from the board in the browser. No API key, no network call.
- “Reset demo data” in the toolbar restores the original sample boards.

## Files

- `index.html` — the whole app (styles and script inlined)
- `CHANGELOG.md` — what changed, what was verified, and next steps
- `LOCAL_AGENT_PROMPT.md` — the brief used for this polish pass
- `SUBMIT_CHECKLIST.md` / `LOOM_SCRIPT.md` — submission notes and video script

## Submit (all three, from mingwsumit@gmail.com)

1. Public GitHub repo: **https://github.com/sumitagg24/atomic-trello-board**
2. Live URL (deployed on Vercel, static, no build command):
   **https://atomic-trello-board.vercel.app** — redeploy with
   `vercel --prod` from this folder after a change.
3. Loom video, under 5 minutes — intro, live demo with a real drag + reload,
   board summary, quick code walkthrough, what you'd improve next
4. Form: https://docs.google.com/forms/d/e/1FAIpQLScSbfBDyyFUZGdntU5GQlKPZlbnErsA8jRfV-cdpzTk8vAb0A/viewform
   — paste the GitHub repo link + live URL + Loom link

Before recording the Loom: open the live URL, drag a card between lists, reload,
and confirm the move persisted. If drag ever misbehaves, open a card and use the
List (or Board) dropdown in its editor — that moves it too.
