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

## Keeping the list calm

Topics are flat rows separated by thin dividers, not boxed cards. A small amber dot marks what's due, and per-row actions (Do today, ×) appear on hover. *Upcoming* is collapsed by default (click it to expand), and long lists show 40 rows at a time with a "Show more" button.

## Editing topics

Click (or tap) a topic's name to rename it in place. Enter or clicking away saves; Escape cancels.

Click the course line under a topic (e.g. `Campbell Biology › Chapter 10`) to move it: pick a chapter to move it down a level, or backspace the chapter to file it under the course alone. Uncategorized topics show "Add to course" on hover. *Select → Move* does the same for many topics at once.

## Reviewing early

Hover an upcoming topic (or look for the faint button on mobile) and click **Do today** to pull its review forward to today. It moves into *Due today*, and grading it schedules the next review from there as usual. An **Undo** message puts it back on its original date.

## Calendar

Switch the view to **Calendar** to see a month grid of what's due. Each day shows how many topics are scheduled, with busier days tinted a little more strongly; overdue topics are counted on today so nothing hides in the past. Click a day to list its topics below the grid (review, rename, and move all work there). The calendar follows the sidebar, so selecting a course or chapter shows just its schedule. It's read-only — the schedule itself comes from your grades.

## Exam dates

Open a course's ✎ dialog and set an **Exam date**. Nothing else to configure: a course with a date is in exam mode, a course without one uses plain SM-2 for long-term retention. You can mix both.

- **Reviews land before the exam.** Normally SM-2 might push a well-known topic 30 days out. With a date set, the next review is capped so it comes up before the exam (the last pass about two days out). The stored interval and ease are untouched, so scheduling picks up normally once the date has passed.
- **Existing schedules are pulled in.** Setting a date moves any review already scheduled past the cap, with an **Undo** message. Clearing the date doesn't move them back.
- **Quick glimpse.** A line above the list shows each upcoming exam in view, e.g. `USABO · exam in 12 days · 18 not yet reviewed · 5 shaky`. Click it to jump to that course. Exams are marked ★ on the calendar.
- **Coming back after a break.** If you haven't reviewed in a week or more and topics are waiting, a gentle note says so. Because everything was already scheduled, you resume where you left off instead of starting over.

## Weakest topics

The **Weakest** view lists what needs the most work, worst first: topics whose last grade was a miss, whose ease has slipped, or that you've missed more than once. Rows show how often a topic was missed. The sidebar tooltip for a course or chapter also counts its shaky topics.

## Linking your notes

Paste a link (`https://…` or an Obsidian `obsidian://` URI) into the topic box, or into a topic's name when renaming it, and it's attached to the topic as a ↗ icon that opens your notes in Notion, Google Drive, Obsidian, and so on. Revisit stays the index and schedule; the notes stay where they are. Delete the link from the name to remove it.

## Importing what you already have

**Import** (next to *Select*) turns an outline or a markdown export into topics in one go, from pasted text or chosen `.md` / `.txt` files:

- `# Heading` is a course, `## Heading` is a chapter.
- Bullets, numbered lines, and deeper headings become topics.
- `[text](url)`, bare URLs, and Obsidian `[[wiki links]]` are handled; links are attached to the topic.
- The path box at the top is the default home for anything not under a heading.
- A preview line shows how many topics will be added and how many already exist (duplicates are skipped). **Undo** removes the import.

Notion, Obsidian, and Google Docs can all export markdown, so there are no integrations or sign-ins.

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
