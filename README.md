# Revisit — Notes Review

A minimalist spaced-repetition tracker for study topics. Add a topic, review it when it's due, and grade how well you recalled it. Scheduling uses the SM-2 algorithm. All data stays in your browser's `localStorage`.

The whole app lives in `index.html` (no framework, no build step required); Vite is only used as a dev server and static bundler.

## Organizing categories

- **Course → Chapter → Topic** — the second box builds the path step by step. Type a course (or pick one from the suggestions) and press Tab or `/`; it becomes a pill and the same box asks for a chapter. Backspace on an empty chapter turns the pill back into text. Topics then show a breadcrumb like `Campbell Biology › Chapter 10`, and the sidebar shows each course as a collapsible parent.
- **Add in context** — when a course or chapter is selected in the sidebar, the box is pre-filled with it, so adding a topic there is just "type the name, press Enter."
- **No more near-duplicates** — suggestions only show what fits the current step (courses, then that course's chapters), and typed names snap to existing casing, so `apush` files under `APUSH`.
- **Rename / merge** — hover a category in the sidebar (or tap the active chip on mobile) and click ✎. Change the name to rename every topic under it, add a `/` to move it under a course, or type an existing name to merge the two.
- **Archive** — from the same edit dialog. Archived categories leave the sidebar, due list, and "All" count, but keep their review history. Find them under "Archived" at the bottom of the sidebar; adding a new topic to one unarchives it.
- **Order** — the sidebar defaults to *Recent* (categories with topics due first, then most recently reviewed/added). Click the label next to "Categories" to switch to *A–Z*.
- **Filter** — once you have 10 or more categories, a filter box appears above the list.

A small amber dot next to a category means it has topics due today.

## Editing topics

Click (or tap) a topic's name to rename it in place. Enter or clicking away saves; Escape cancels.

Click the course line under a topic (e.g. `Campbell Biology › Chapter 10`) to move it: pick a chapter to move it down a level, or backspace the chapter to file it under the course alone. Uncategorized topics show "Add to course" on hover. *Select → Move* does the same for many topics at once.

## Selecting and clearing

- **Select** (next to the sort control) turns rows into checkboxes and shows a bar with *Select all*, *Move*, *Delete*, *Clear all*, and *Done*. Escape also exits.
- **Move** re-files the selected topics under any course/chapter in one step.
- **Delete** and **Clear all** ask for confirmation first. *Clear all* follows what you're viewing: with a course selected it clears only that course; with *All* selected it clears everything except archived categories.
- Every delete — including the × on a single topic — shows an **Undo** message for a few seconds.

## Run locally

```bash
npm install
npm run dev      # http://localhost:4317
```

`npm run build` writes a static bundle to `dist/`. You can also open `index.html` directly in a browser.

Data from earlier versions (stored under `recall_topics_v1`, from when the app was called Recall) is picked up automatically.
