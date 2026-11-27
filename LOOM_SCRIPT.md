# Atomic Boards — Loom script (final teleprompter)

**Live app:** https://atomic-trello-board.vercel.app  
**Repo:** https://github.com/sumitagg24/atomic-trello-board  
**Target length:** 4:55 (hard cap 5:00)  
**Format:** screen + mic + camera bubble, 1080p, client-call tone

> Dry-run verification (2026-11-27, live Vercel URL): reset-demo flow, board switching, card editor/checklist save (3/3), native HTML5 drag-event move (Backlog → Doing, verified with synthetic dragstart/dragover/drop dispatch in browser; record with a real mouse drag), reload persistence, Overdue filter (2 overdue cards), summary panel numbers/action, cross-board drag to Marketing Site Refresh tab landing in Ideas, and code line refs (`var LS_KEY`, `function render(`, `Drag and drop (native`, `function buildSummaryData`) all confirmed on the live app. Reset demo data after the dry run.

---

## Pre-flight (do before you hit record)

**Record at desktop width with the summary panel open** — the panel hides itself at **860px or narrower** (`index.html:2607`: `innerWidth <= 860`), and its 336px (`index.html:402`) is what pushes the **Done** column off a 1440×900 window: maximize instead.

1. Open **https://atomic-trello-board.vercel.app** in Chrome. **Maximize** the window (not 1440×900) at 100% zoom — at 1440 the **Done** column is clipped and you would be dragging while horizontal-scrolling.
2. Make sure the theme is **light**: if dark, click the sun/moon button at top right (next to “✦ Board summary”) until the page is white.
3. Click **Reset demo data** (under the filter row, left side). In the dialog click **Delete**. Wait for the toast “Demo data restored”.
4. Confirm the right-hand **✦ Board summary** panel is visible. If it is collapsed the window is 860px or narrower: widen the window, then click **✦ Board summary** at top right — that click pins the panel open for the rest of the session, so a later resize cannot re-hide it.
5. Open VS Code with `atomic-trello-board/index.html`. Increase font size (`Ctrl` + `+`) so code is readable at 1080p. Close the terminal panel.
6. Loom: screen + microphone + camera bubble, 1080p. Turn off notifications (Windows Focus assist / Do not disturb).
7. Keep this teleprompter on a phone or second screen.
8. Optional 10-second test recording, then delete it.

**Three traps that cost a take:**

- **Browser zoom is width.** `Ctrl` + `+` in Chrome shrinks the viewport and hides the panel, and at 1440 wide the **Done** column is already clipped by ~108px. Maximize, leave browser zoom at 100%, and zoom VS Code instead.
- **Hover-only buttons.** Card **⋯** buttons are invisible until you hover the card (`index.html:334`–`337`) — park the cursor on the card before you mention the card menu.
- **The panel scrolls.** It holds ~1050px and scrolls inside itself below ~1110px window height, so at 900px tall the last three **needs attention** rows are out of view — scroll it ~200px when you reach them.

**On-screen state when you start:** Product Launch board, light theme, summary panel open, all filters cleared, no dialogs.

---

## 5-minute teleprompter

Read the quoted lines. Do the bracketed action at the same time. Pause one beat after each click.

### 0:00–0:15 — Intro

*Screen: live app, address bar visible.*

> “Hi, I’m Sumit. This is Atomic Boards — a Trello-style board manager I built for the Atomic Computing build task. It’s live on Vercel at atomic-trello-board.vercel.app, and it’s a single static HTML file with no backend.”

### 0:15–0:30 — Boards

*Click the **Engineering Sprint** tab. Pause 1 second. Click **Product Launch**.*

> “It has boards, lists and cards, saved in the browser. Here are three seeded boards, and switching between them is instant.”

### 0:30–0:55 — Card editor + checklist

*In the **Doing** list, click the card titled **“Landing page hero + screenshots”**.*

> “Cards open in an editor with a description, due date, labels, an assignee and a checklist. This one is at two of three.”

*In the editor, click the last checklist checkbox, **“Check the mobile crop”**. Point at the “3/3” progress. Click **Save changes**.*

> “I’ll tick the last item — the card face now shows three of three.”

### 0:55–1:15 — Drag between lists

*Drag **“Competitor pricing teardown”** from **Backlog** into **Doing**, above the first card. Show the drop line before releasing.*

> “Dragging uses native HTML5 events. The line shows exactly where the card will land, and the move is saved immediately.”

### 1:15–1:25 — Reload persistence

*Press **Ctrl+R**. Wait for the page. Point at “Competitor pricing teardown” now in Doing.*

> “Reload — it’s still there, because every change writes to localStorage.”

### 1:25–1:40 — Filters

*Click the **Overdue** chip. Point at the two red cards. Click **All cards**.*

> “Filters cover overdue, due soon and labels. Two cards are overdue, and the board marks them in red.”

### 1:40–2:40 — Bonus summary

*Point at the right-hand panel, top to bottom as you speak.*

> “The bonus feature is this board summary. It updates live: total cards, completion, overdue, due in the next two days, unassigned, and cards per list. It also finds the busiest list, lists what needs attention, and suggests one next action — here it points at the most overdue card. All of it is computed in the browser from the board data, with no API key and no paid service.”

### 2:40–3:00 — Cross-board drag

*Drag **“Beta feedback synthesis”** from Backlog onto the **Marketing Site Refresh** tab. Release when the tab highlights.*

> “Dropping on another board’s tab moves the card across boards. It lands in Marketing’s Ideas list, and both activity logs record the move.”

*Click the **Marketing Site Refresh** tab. Point at the card in Ideas.*

> “There it is, in the other board.”

### 3:00–3:10 — Back to the main board

*Click **Product Launch**.*

> “Back on Product Launch — now the code.”

### 3:10–4:15 — Code walkthrough (VS Code)

*Alt+Tab to VS Code, with `index.html` open.*

> “Everything is in one index.html. The state is boards, lists and cards, with a version and the active board id.”

*Ctrl+F, type `var LS_KEY`, press Esc. Point at the storage lines.*

> “Data lives under one localStorage key, and save and load are right here.”

*Ctrl+F, type `function render(`, press Esc. Point at the function.*

> “Every change goes through render, which rebuilds the view and then saves.”

*Ctrl+F, type `Drag and drop (native`, press Esc. Point at the drag section.*

> “The drag handlers are native dragstart, dragover and drop, with two functions doing the data move — one inside a board, one across boards.”

*Ctrl+F, type `function buildSummaryData`, press Esc. Point at the function.*

> “The summary is plain rules over the same data — overdue, due soon, unassigned, busiest list and the next action. No model, no API call.”

### 4:15–4:40 — What you would improve

*Alt+Tab back to the app.*

> “Next I’d add a backend with real accounts and role-based access, so boards sync across devices. I’d also add an LLM-backed summary with a proper key, and split the single file into modules with tests.”

### 4:40–4:55 — Close

*Point at the address bar.*

> “The repo and live URL are in the submission form. Thanks for watching.”

*Stop the recording.*

---

## If something goes wrong (say the line, keep moving)

| Problem | Fix | Line to say |
| --- | --- | --- |
| Drag doesn’t pick up | Click the card → change **List** in the editor → **Save changes** | “There’s also an editor fallback for moving cards — I’ll use that.” |
| Drop lands in the wrong spot | Drag it again, or say it moved and continue | “Close enough — the drop line shows the exact insertion point.” |
| Summary panel is hidden | Click **✦ Board summary** at the top right | “The summary panel is collapsible.” |
| Wrong theme on screen | Do not fix on camera; keep going | Nothing — finish and re-record only if it looks bad |
| You run past 4:50 | Skip the filters (1:25–1:40) or shorten the improvement list | — |
| VS Code opens the wrong tab | `Ctrl+P`, type `index.html`, Enter | — |

**Hard rule:** stop by 4:55 even if you skip a section. A clean 4:30 beats a rushed 5:30.

---

## After recording

1. In Loom, trim the first/last second if needed. Title it **“Atomic Boards — Atomic Computing build task”**.
2. Set visibility to **Anyone with the link**.
3. Copy the **share** URL (`https://www.loom.com/share/...`).
4. Fill the submission form (email `mingwsumit@gmail.com`, full name, repo, live URL, Loom, bonus **AI board summary**, host **Vercel**, AI tools, anything else).
5. Submit, then screenshot the confirmation.
6. Keep the repo and live URL unchanged until the reviewer opens them.

## Final checklist

- [ ] Loom under 5:00 and plays logged-out
- [ ] Form email = application email
- [ ] Full name complete
- [ ] Repo + live + Loom links pasted
- [ ] AI board summary + Vercel selected
- [ ] Confirmation screenshot saved
