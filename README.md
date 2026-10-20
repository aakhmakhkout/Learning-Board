# Learning Board

A single-file planner for any learning roadmap. Pin notes on a cutting-mat board, tick tasks in a handwritten notebook, track dates on a timeline, and keep every topic as a file you can open and close. Load your own plan from one JSON file.

No build step, no dependencies, no account. Progress is saved in your browser's `localStorage`.

## Features

- **Pinboard:** draggable cut-paper notes, plus your own notes.
- **Notebook:** a book with one page spread per phase. Add pages, headings, dates, phase tags, text, checkboxes, bullets and sticky notes on either side.
- **Timeline:** week strip, per-phase dates, hours, deliverables and progress.
- **Files:** every task as a file icon, split into open and closed. Open one for details, reading links and your own notes, then close it.
- **Self-adjusting dates:** a task that is not ticked by its end date keeps today as its end date, and everything after it moves. Each phase also has +1 / −1 day buttons.
- **Data:** paste a JSON file to replace the whole plan (see below).
- **Light and dark** themes.

## Run it

Open `index.html` in a browser. To host it, enable GitHub Pages for this repo (Settings → Pages → deploy from the `main` branch, root folder).

## Use your own plan

1. Copy the prompt below into an AI assistant and fill in the `[brackets]`.
2. Copy the JSON it returns.
3. In the app, open **Data**, paste it, and press **Apply data**. A `.json` file can be loaded with **Load .json file**.

Applying data replaces the plan and clears progress, pins and notebook pages, so do it once at the start. **Copy** in the Data panel shows the current plan, which is a good base to edit by hand. **Reset to demo data** brings the example back.

### The prompt

````text
Hello Claude! I use a planner web app called Learning Board:
https://github.com/aakhmakhkout/Learning-Board
It loads a learning plan from a JSON data file. Please create that file for me.

ABOUT ME
- Goal: [e.g. become job-ready as a MERN stack developer]
- What I'm learning: [MERN stack / DevOps / Python / ...]
- What I'm following: [roadmap link / YouTube video or playlist link / syllabus text]
- Where I am now: [what I already know or have finished]
- Start date: [YYYY-MM-DD]
- Time: [number] weeks, [number] hours per day
- Name for the board: [first name]
- Skip or focus on: [optional]

HOW TO WORK
1. If you can open links, read the repo's README and data.example.json first. If you can't, use the format below.
2. Analyse the roadmap / video / syllabus I gave. If you can't open it, say so and ask me to paste the chapter list or syllabus. Never invent chapters.
3. Split the material into 4 to 8 phases, in learning order. Give each phase 3 to 6 tasks.
4. A task is a short title naming the concrete topics, plus "days" (a whole number, at least 1). Be realistic for my hours per day.
5. The total of all days must fit my time window with about 10% buffer. Cut or merge low-priority topics rather than overrunning. Put "(optional)" in the title of nice-to-haves.
6. For each phase add: goal (one sentence), deliverable (something concrete I will have built or finished), tip (one specific warning), and resources (names that match a "topic" in the top-level resources list).
7. Add a "parallel" track only if it helps (for example DSA or daily practice), otherwise set it to null. "startDay" is how many days after the start date it begins.
8. Add 2 to 3 projects, 6 to 9 short notes, and 5 to 8 resource topics with 2 to 3 links each. Use only official or well-known free links you are sure exist. If unsure, leave the link out.
9. Reply with ONE JSON code block that is valid JSON (no comments, no trailing commas). After it, add at most 3 short lines listing the assumptions you made.

FORMAT
{
  "meta": { "name": "Asha", "title": "Learn Python", "tagline": "One sentence about the plan.", "startDate": "2026-11-02", "hoursPerDay": 3 },
  "phases": [
    {
      "name": "Python basics",
      "color": "#d9432a",
      "goal": "One sentence.",
      "deliverable": "Something concrete.",
      "tip": "One warning.",
      "resources": ["Python docs"],
      "tasks": [ { "title": "Syntax, types, loops", "days": 3 } ]
    }
  ],
  "parallel": {
    "tag": "DSA", "name": "Practice track", "intro": "One sentence.", "startDay": 10,
    "resources": [], "details": [ { "label": "Block", "text": "Evening, 45 min" } ],
    "items": [ { "title": "Arrays and strings", "days": 7 } ]
  },
  "projects": [ { "title": "Project name", "text": "One sentence." } ],
  "resources": [ { "topic": "Python docs", "links": [ { "title": "Tutorial", "url": "https://docs.python.org/3/tutorial/" } ] } ],
  "notes": [ { "title": "Daily rhythm", "text": "Short tip." } ]
}
````

## Data format

| Field | Notes |
| --- | --- |
| `meta.name` | Shown next to the logo; the first letter becomes the logo. Up to 24 characters. |
| `meta.title` | Big heading. The last word is highlighted. |
| `meta.tagline` | One line under the heading. |
| `meta.startDate` | `YYYY-MM-DD`. Required. |
| `meta.hoursPerDay` | A number, used for the hours estimate. |
| `phases[]` | Required, 1 to 12. Each has `name`, optional `color` (`#rrggbb`), `goal`, `deliverable`, `tip`, `resources` (topic names), and `tasks`. |
| `phases[].tasks[]` | 1 to 25 per phase. `title`, and `days` (whole number, 1 to 60). Phases run one after another. |
| `parallel` | Optional second track that runs beside the phases. `tag`, `name`, `intro`, `startDay`, `resources`, `details[]` (`label`, `text`) and `items[]` (same as tasks). Use `null` to leave it out. |
| `projects[]` | Up to 8. `title`, `text`. |
| `resources[]` | Up to 14 topics, each with up to 8 `links` (`title`, `url`). Only `http` and `https` links are kept. |
| `notes[]` | Up to 24 pinboard notes. `title`, `text`. |

See `data.example.json` for a full working file.

## Files

- `index.html`: the whole app.
- `data.example.json`: the demo plan, in the format above.
- `LICENSE`: MIT.

## Author

Made by **Noumaan Nabi** ([@aakhmakhkout](https://github.com/aakhmakhkout)).

## License

MIT. See [LICENSE](LICENSE).
