# CHANGELOG

All work stayed inside `index.html` — one static file, no backend, no database,
no API key, no build step. The 3 seed boards / 23 cards, the label filters,
search and the on-device board summary were kept and extended, not replaced.
The look was then reworked: the original deep-ocean gradient and frosted glass
are gone, replaced by a white-first palette with a matching dark theme (see
*Restyle* below).

## Brief compliance pass (26 Nov)

- **Drag and drop uses native HTML5 drag events.** Cards are `draggable="true"`;
  `dragstart` stores the card id, `dragover` on a list paints the drop line,
  `drop` performs the move, and dropping on a board tab moves the card to that
  board. The earlier pointer-event drag was removed so the implementation matches
  the brief's `dragstart` / `dragover` / `drop` requirement exactly.
- **Due soon is 2 days**, as the brief specifies (it had been 3). The card badge,
  the filter, the match text and the summary stat all use the same `dISO(2)`
  limit, so they cannot disagree.
- **Deleting a list asks for confirmation** before its cards are removed, then
  keeps the 5-second undo behind it.
- **Cards store `labels[]`** instead of one `label`, so a card can carry several
  labels. The editor's swatches toggle on and off, the label filter matches any
  of them, and saved or imported cards in the old single-`label` shape are
  migrated automatically by `normalizeCard()`.

## Review pass and deployment (26 Nov)

- **Drag cleanup.** `clearDropUI()` clears `.drag-over` / `.drop-target` in one
  DOM pass, the drop line is reused while the pointer stays inside one list
  instead of being destroyed and re-created on every `dragover`, and the board
  tab highlight no longer churns its classes on each event. The duplicate
  `.cards.drag-over` background rule was collapsed into one.
- **Labels cleanup.** `normalizeCard()` now drops duplicate and unknown label
  names as well as migrating the old single `label`, so imported or previously
  saved cards always end up with a clean `labels[]`.
- **Deployed.** Public static deployment on Vercel:
  https://atomic-trello-board.vercel.app — no build step, and `.vercelignore`
  keeps the notes and screenshots out of the upload.
- **Re-verified on the live URL:** moved a card Backlog → Doing with HTML5 drag
  events, reloaded, and the move persisted; the summary still reads "Due in 2
  days", 3 boards / 23 seed cards, and the console stayed clean.

## Fixed

- **Drag and drop.** Cards move between lists, reorder inside a list, and move to
  another board when dropped on its tab. The drop line follows the cursor, the
  board and long lists auto-scroll, and the source card stays dimmed. (This pass
  first used pointer events; the compliance pass above moved it to the native
  HTML5 drag events the brief asks for.)
- **Dialog stacking.** A dialog opened from another dialog (e.g. "delete forever"
  from the archive, or the delete-card confirm) could render behind the first
  one. Overlays now get an increasing z-index on open and Esc closes the topmost.
- **Card editor footer.** Save/Cancel/Archive/Delete could sit below the fold on
  short screens. Modals now have a scrollable body and a pinned action footer.
- **Checklist text styling.** Checklist items inherited the uppercase,
  letter-spaced field-label style; they now render as normal sentence-case text.
- **Focus/search styling in dark mode.** The search field no longer turns into a
  white box on focus in dark mode, and uses the same focus ring as the rest.
- **Small-text contrast.** Muted text (`--ink-3`) was darkened in light mode and
  lightened in dark mode to clear AA for the 11–12px labels.
- **Summary panel on resize.** If the panel was collapsed at phone width it stayed
  collapsed after growing the window; it now reopens on desktop unless you closed
  it yourself.

## Added

- **Due dates** on every card with red **overdue** and amber **due-soon** badges,
  plus **Overdue** and **Due soon** filters (chips in the filter row).
- **Checklists** inside cards: add/tick/remove items, a progress bar in the
  editor and a `2/5` chip with a mini progress bar on the card face.
- **Archive**: archive a card from its editor, browse the archived view, restore
  it to its original list, or delete it permanently.
- **Activity log per board** (created / moved / edited / archived / restored /
  deleted, with relative and absolute times), written on every mutation.
- **Duplicate board** (fresh ids for every list, card and checklist item).
- **Two starter templates** — *Product launch* and *Study plan* — offered in the
  New board dialog and from an empty board, alongside the blank 3-list board.
- **Export / import JSON** for a board, from the board menu; imported boards get
  fresh ids and are validated/normalised before they are added.
- **Keyboard shortcuts**: `N` new card, `/` search, `Esc` close dialog/menu or
  clear filters. Ignored while typing; there are on-screen hints under the title.
- **Cross-board dragging** onto the board tabs at the top, plus **Board** and
  **List** selectors in the card editor as the keyboard/touch-safe fallback.
- **Assignee** as a free-text name with suggestions (no accounts), with initials
  avatars and a deterministic colour per name.
- **Card count** on every list header (shows `matching/total` while filtering).
- **Undo for deletions**: deleting a card or a list shows a toast with **Undo**
  for 5 seconds and restores the exact prior state.
- **Real empty states**: empty list (with an add-card action), empty board (add a
  first list, or apply a template), and no search/filter results (with a clear
  action) — plus empty states for the archive and the activity log.
- **Board menu** (⋯) grouping rename, duplicate, templates, archive, activity,
  export, import and delete.

## Restyle — white and dark theme

- **One palette, two skins.** Every colour now comes from CSS custom properties:
  a white-first light theme (white cards, header and panels, `--list-bg:
  #f7f9fc`, `--line: #e3e8ef` borders) and a black dark theme (black page,
  `#101010` lists, `#171717` cards, `#0b0b0b` summary panel, neutral grey borders
  and washes — no blue cast on any surface; only the accent and the wordmark
  carry colour). Components no longer hard-code colours.
- **System preference, with an override.** Dark mode is no longer a
  `@media (prefers-color-scheme: dark)` block; it is driven by
  `html[data-theme="dark"]`, so the header's new sun/moon button can override the
  system setting. The choice is saved in `localStorage` under
  `atomic-boards-theme` and falls back to the system preference the first time.
- **No flash of the wrong theme.** A small inline script in `<head>` applies the
  saved theme before the first paint.
- **No hard-coded colour left in components.** Raw hex/rgba values were lifted
  out of every rule into tokens with a light and a dark value: surfaces, text,
  accent, the three status pairs, interaction greys, shadows, `--on-label` for
  text on saturated fills, `--mark-*` for the wordmark, `--toast-bg/-ink`, and
  `--canvas-top/-bottom` + `--wash-a/-b` for the page background. A theme change
  is now a token change, so nothing can drift between modes.
- **One token set, 47 names, no aliases.** The tokens live in a single `:root`
  and a single `html[data-theme="dark"]` block. Duplicates were collapsed into
  the values they shadowed: `--canvas-ink*` → `--ink*`, `--drop` → `--accent`,
  `--on-accent` → `--accent-ink`, `--scroll-card*` → `--scroll*`,
  `--shadow-input`/`--shadow-avatar` → `--shadow-pop`/`--shadow-card`. Values
  that only wrapped one consumer are now written at the point of use — the
  gradient ends (`transparent`), `::selection`, the active-tab count, and the
  toast's border, glow and Undo button all derive from `--accent` / `--toast-ink`
  with `color-mix()` instead of owning a token each (that removed 19 tokens of
  the 66 the first pass left behind).
- **Its own identity, not a skin of someone else's product.** The chrome no
  longer labels itself as a Trello copy: the page is titled **Atomic Boards**
  with the line "Boards, lists and cards — saved here", its own mark and its own
  palette. The board → list → card model stays because the brief asks for it —
  the design, not the product type, is what's original.
- Recoloured for both themes: page gradients, header and tabs, filter chips,
  buttons, the search field (its SVG icon now uses `currentColor`), card/list
  shadows, empty states, dialogs and scrims, and the summary panel.

## Polished

- Structural inline styles left in the rendered markup were moved into classes
  (`.form-row`, `.empty-hint.tall`, `.confirm-text`, `.attn-link`,
  `.field-hint.tight`); the only inline values left are data (label colours,
  avatar colours, progress widths).

- Responsive layout: on phones the board keeps scrolling **horizontally** with
  snap points (instead of stacking every list), cards stay readable at
  `min(84vw, 320px)`, the header and filter row scroll horizontally, and modals
  fit the viewport with a pinned footer.
- Consistent hover / active / focus-visible states for buttons, chips, tabs,
  cards, list titles and cards' edit affordances.
- Card lift on hover, a dashed "hole" and dimmed source while dragging, drop-line,
  list and board-tab drop highlights, landing pulse, animated dialog open and
  menu pop-in — motion is reduced under `prefers-reduced-motion`.
- Dialogs trap Tab focus, restore focus to the trigger on close, and close on
  backdrop click or Esc.
- Board title and list titles remain click-to-rename (keyboard accessible).

## Verification performed (Chromium, final build)

- Dragged a card Backlog → Doing with dispatched HTML5 drag events (`dragstart`
  / `dragover` / `drop`): dimmed source + drop-line observed; the card moved and
  the order persisted through a reload from `localStorage`.
- Dragged a card onto another board tab: tab highlighted, card landed in the
  target board's first list, and both boards' activity logs recorded the move.
- Card editor fallback: changed **List** and saved — card moved and persisted;
  checklist item added and ticked — saved and reflected as `1/4` on the card.
- Archived a card, opened the archive, restored it; delete card + confirm, then
  **Undo** from the toast restored the card.
- Overdue filter showed exactly the 2 overdue cards; a nonsense search showed the
  "No cards match" panel and clearing restored all 11 cards.
- `N` focused a card composer, `/` focused search, `Esc` closed the card editor.
- Empty board: deleted all lists → empty state with the add-list form and both
  template buttons; applied the Study plan template (4 lists, 5 cards).
- Created a board from the Study plan template and duplicated it (no id
  collisions, 4 lists / 5 cards copied, new board active).
- Exported a board (blob download `algorithms-study-copy.json`) and imported a
  JSON board through the real file input: lists, due date, label, assignee and
  checklist all restored.
- 390×844 viewport: no page-level horizontal overflow, lists scroll horizontally,
  the card modal fits (370×820 in 390×844) with visible actions and a scrolling
  body.
- Theme toggle: switched dark → light from the header, computed colours changed
  as expected and the choice survived a reload; the card editor and the 390×844
  viewport were re-checked in the light theme (toggle visible, no horizontal
  overflow).
- Token audit: every `var(--…)` in the stylesheet and script resolves to a
  declared token (47 declared, 47 used, none undefined or orphaned), and a fresh
  probe element reports the dark accent/ink pair in dark mode — so no component
  falls back to a light-theme colour.
- 390×844 after the rename: no page-level horizontal overflow, the longer
  "Atomic Boards" wordmark fits beside the theme button.
- No console errors on load or during any of the flows above.

## Visual review (screenshots, not just computed styles)

Captured and looked at at 1280×820 and 390×844, light and dark, plus the card
editor in both themes. Three things only the pictures showed:

- **"Cards per list" bars were invisible.** `.bar-fill` is a `<span>` and had no
  `display`, so the inline element ignored `height`/`width` and every bar rendered
  0 px wide. It is `display:block` now and the bars fill correctly.
- **Duplicate rows in "Needs attention".** A due-soon card with no owner appeared
  twice (once as DUE SOON, once as NO OWNER). The three groups now dedupe by card
  id, first tag wins.
- **Orphaned ⋯ on phones.** The board-menu button wrapped onto a line of its own
  under the title at 390 px. The title now takes a full row and the three
  toolbar actions sit together, right-aligned. The search field also takes the
  full row so the summary/theme buttons wrap as a right-aligned pair instead of
  leaving a ragged gap.
- **Marketing label contrast.** White on `#d97004` was 3.35:1. The label/avatar
  colour is now `#b45309` (5.02:1 with white) — still clearly orange next to the
  red Bug and green Launch chips.
- Checked and left alone: the wordmark (mark tile + name + subtitle align on a
  34 px tile), the two-row desktop header, the wrapped "Content" filter chip, and
  the summary's "(+1 more overdue)" phrasing.

Not checked: a physical mouse drag by hand, Safari/Firefox, and a screen reader.
Dragging uses the browser's native HTML5 drag events, so it needs a mouse or
trackpad; on a phone, move a card via the editor's **Board**/**List** selectors
(tapping a card opens the editor).

## NEXT STEPS FOR ME

1. Push this folder to a new **public** GitHub repo (`index.html` at the root).
2. Deploy it free on Vercel as a static site (no build command, no output dir).
3. Open the live URL, drag a card between two lists, reload, and confirm it stuck.
4. Record the Loom (< 5 min): intro → drag + reload → board summary → one code
   walkthrough → what you would improve next. New material worth showing:
   overdue filter, checklist progress, archive/restore, activity log, undo toast,
   cross-board drag, templates and JSON export/import.
5. Submit the repo link + live URL + Loom link at
   https://docs.google.com/forms/d/e/1FAIpQLScSbfBDyyFUZGdntU5GQlKPZlbnErsA8jRfV-cdpzTk8vAb0A/viewform
   (deadline Mon 30 Nov 2026).
