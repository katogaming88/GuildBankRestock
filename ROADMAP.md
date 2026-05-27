# Roadmap

Planned work for GuildBankRestock. Items move into GitHub issues when active, and into CHANGELOG.md when shipped.

Current version: 0.9.12

---

## v1.0 -- Run feedback and visual polish

Small, self-contained improvements to the post-run experience and item list readability.

- [ ] **Per-item cost in log** -- the Log tab currently records "Bought 5x Flask of X" but not
  the price paid. Store the unit price at purchase time and include it in the log entry
  ("Bought 5x Flask of X at 120g each -- 600g total"). Keeps per-item spend visible without
  spamming chat.

- [ ] **Pricing tooltip** -- show the last recorded purchase price when hovering an item row
  (e.g. "Last bought at 120g per unit on 05/22 14:31"). Requires storing per-item last-price
  and timestamp in SavedVariables after each confirmed purchase.

- [ ] **Color coding by AH availability** -- after a search completes, color item rows by
  result: green = found on AH, red = not found, grey = disabled/unticked. Clears back to
  default when a new search starts. Gives instant visual feedback without needing to read
  the log.

---

## v1.1 -- Accounting tab

Priority feature: a persistent history of every restock run showing what was bought, what
was missing, and what it cost.

- [ ] **Run history in SavedVariables** -- on run completion, append a structured record to a
  new `runs` array: timestamp, context (guild/personal), mode, list of items bought (name,
  qty, unit price, total cost), items not found on AH, items skipped (price limit), and
  total gold spent. Cap at a reasonable number of records (e.g. 50 runs) to avoid SavedVars
  bloat.

- [ ] **Accounting tab UI** -- add an "Accounting" entry to the sidebar (alongside Log and
  About). The tab shows a scrollable list of past runs, newest first. Each run shows:
  date/time, context, total gold spent, and an expandable row listing each item purchased.
  A "Clear History" button at the bottom wipes the `runs` array.

---

## v1.2 -- Low Stock mode and UI density

- [ ] **Low Stock mode** -- a sub-option in Restock mode that automatically enables only the
  items that are below their target quantity and disables the rest. Saves the step of
  manually unticking fully-stocked rows before starting a run. Toggle in the sidebar next
  to the existing Restock / Bulk buttons.

- [ ] **Compact row mode** -- an option to toggle between the current expanded row layout
  and a tighter compact view that fits more items on screen without scrolling. Compact mode
  hides less-used columns (e.g. Est g) and reduces row height.

---

## Backlog (unscheduled)

- **Food category** -- populate Categories/Food.lua with verified Midnight raid food item
  IDs once they are confirmed in-game. Until then the category remains hidden (empty
  categories are already filtered from the sidebar).
- **Profile import/export** -- serialize a profile to a pasteable string for sharing
  loadouts between officers.
- **Per-tab guild bank targeting** -- restrict a restock run to items missing from a
  specific bank tab rather than scanning all tabs.
