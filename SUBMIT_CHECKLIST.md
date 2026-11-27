# Atomic Computing — submit the build task (due Mon 30 Nov, aim Sun 29 Nov)

Status at Wed 26 Nov 2026: the app is built and deployed at
https://atomic-trello-board.vercel.app (Vercel, static, no build). Drag-and-drop
was verified there in a real browser — a card moved between lists and onto
another board's tab, and the move survived a reload. It uses native HTML5 drag
events (dragstart / dragover / drop) with a drop line showing where the card will
land; on touch devices use the Board / List dropdowns. Fallback if drag ever
misbehaves: open a card, change its List (or Board) dropdown in the editor,
save — that moves it too.

## 1. GitHub repo — done

Public repository: **https://github.com/sumitagg24/atomic-trello-board**

The whole app is one self-contained file, committed at the repo root:
`index.html` (the docs and screenshots sit alongside it).

To ship a change: `cd atomic-trello-board && git add -A && git commit -m "..." && git push`

## 2. Vercel deploy — done

Already deployed from this folder with the Vercel CLI:

- Live URL: **https://atomic-trello-board.vercel.app**
- To ship a change: `cd atomic-trello-board && vercel --prod`
- Only `index.html` is uploaded; `.vercelignore` keeps the notes and screenshots
  out of the public deployment.

## 3. Record the Loom (under 5 min, facecam, your voice)

Script is already written in `LOOM_SCRIPT.md` (same folder as `index.html`):
intro (0:00–0:30) → live demo incl. a drag and a reload (0:30–2:00) → board
summary panel (2:00–3:30) → code walkthrough, all of it in the single
`index.html` (3:30–4:30) → what you'd improve next (4:30–5:00). Record it the way
you'd show up to a client call. Keep it under 5 minutes.

## 4. Submit the form (same email as the quiz: mingwsumit@gmail.com)

https://docs.google.com/forms/d/e/1FAIpQLScSbfBDyyFUZGdntU5GQlKPZlbnErsA8jRfV-cdpzTk8vAb0A/viewform

Paste: public GitHub repo link + live Vercel URL + Loom link.

## Checklist

- [x] GitHub repo public, `index.html` in it (https://github.com/sumitagg24/atomic-trello-board)
- [x] Vercel live URL opens logged-out (https://atomic-trello-board.vercel.app)
- [x] One real drag tested on the live URL + reload persists
- [ ] Loom recorded, under 5 min, at desktop width with the ✦ Board summary panel open (it auto-hides at 860px or narrower; Chrome at ~1440×900, zoom 100%)
- [ ] Form submitted by Sun 29 Nov (hard deadline Mon 30 Nov)
