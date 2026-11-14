# Revisit — Notes Review

A minimalist spaced-repetition tracker for study topics. Add a topic, review it when it's due, and grade how well you recalled it. Scheduling uses the SM-2 algorithm. All data stays in your browser's `localStorage`.

The whole app lives in `index.html` (no framework, no build step required); Vite is only used as a dev server and static bundler.

## Organizing categories

- **Nesting with `/`** — type `Campbell Biology / Chapter 4` in the category box. The sidebar shows `Campbell Biology` as a collapsible parent with `Chapter 4` beneath it. Selecting a parent shows every topic in it and its units.
- **No more near-duplicates** — the category box autocompletes existing courses (including `Course / ` prefixes), and typed names snap to existing casing, so `apush` files under `APUSH`.
- **Rename / merge** — hover a category in the sidebar (or tap the active chip on mobile) and click ✎. Change the name to rename every topic under it, add a `/` to move it under a course, or type an existing name to merge the two.
- **Archive** — from the same edit dialog. Archived categories leave the sidebar, due list, and "All" count, but keep their review history. Find them under "Archived" at the bottom of the sidebar; adding a new topic to one unarchives it.
- **Order** — the sidebar defaults to *Recent* (categories with topics due first, then most recently reviewed/added). Click the label next to "Categories" to switch to *A–Z*.
- **Filter** — once you have 10 or more categories, a filter box appears above the list.

A small amber dot next to a category means it has topics due today.

## Run locally

```bash
npm install
npm run dev      # http://localhost:4317
```

`npm run build` writes a static bundle to `dist/`. You can also open `index.html` directly in a browser.

Data from earlier versions (stored under `recall_topics_v1`, from when the app was called Recall) is picked up automatically.
