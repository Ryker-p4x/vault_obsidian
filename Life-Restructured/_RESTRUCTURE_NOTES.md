# Restructure notes (review this, then delete)

This copy was built from `Life` on the agreed plan. Nothing here is final — edit freely.

## Round 2 — robustness
- **Class notes now support many tasks.** `Templates/Class.md` is a frontmatter + `## Tasks` list; add as many `- [ ]` lines as you want. Dashboard counts open tasks per class and shows the next due date.
- **New frontmatter convention:** `type` + `status` on every content note (see `Templates/_About.md`). Status values: `active`/`done`/`paused`/`someday`.
- **New `Templates/Daily.md`** for the Days/ folder.
- **Project template** gained `area` and `due`.
- **Dashboard** gained a **Deadlines** section and a smarter **Per-class now** (open count + next due). Active projects now reads real `status` and shows a `due` column.
- **Renamed** the two clashing `Overview.md` files to `Debugging Overview.md` and `Study Methods Overview.md`.
- **Fixed** an unclosed cpp code fence in `Validating your code flow.md`.
- **Empty `- [ ]` placeholders removed** from templates — they were inflating task counts.

## Round 3 — configuration & templates
- Core **Daily Notes** plugin wired to `Days/` + `Templates/Daily` (`YYYY-MM-DD`) via `.obsidian/daily-notes.json`.
- New templates: **Book**, **Track**, **Weekly Review**.
- **`.gitignore`** added for a future `git init` (ignores workspace/cache/trash).
- Dashboard: added **Recently completed**, **Needs attention**, and a conventions link up top.
- **Tag scheme** documented in `Templates/_About.md`.

## What moved where

| Old | New |
|---|---|
| `NVIM Environment Plan.md`, `Github Environment Plan.md` (root) | `Plans/` |
| `Notes on Self-Improvement/Full Plan to Programming.md` | `Plans/` |
| `Classes/*.md.md` | `Classes/*.md` (double extension fixed) |
| `Classes/What's this?.md` | `Classes/_About.md` |
| `Projects/What's this?.md.md` | `Projects/Coding/_About.md` |
| `Knowledge/Programming/learncpp.com/Debugging/**` | `Knowledge/Programming/C++/Debugging/` (flattened) |
| `Knowledge/Programming/OverTheWire/...` | `Knowledge/Programming/Security/` |
| `Workflow/**` + `Annoying things in lazy vim.md` + `How to use the programming environment.md` | `Knowledge/Programming/Environment/` |
| `Knowledge/Books/Ne Obliviscaris/` | `Projects/Ne Obliviscaris/` (it's your writing, not a book you read) |
| `Knowledge/{truco,brainmax,read people}` | `Knowledge/Life Skills/` |
| `Notes on Self-Improvement/{progress,typing,neetcode}` | `Self-Improvement/Progress/` |
| `Notes on Self-Improvement/{Exercise*}` | `Self-Improvement/Fitness/` |
| `Notes on Self-Improvement/{Videos,Ideas,Next Steps}` | `Inbox/` (to triage) |

## Deleted (empty / no information)
- `Knowledge/Untitled.md`
- `Guide on how to use this workflow.md`
- `Studying for Geography.md` → became `Classes/Geography.md`

## Merged
- The two `Drawbacks.md` (basic techniques + printing) are now one note with two headings.

## Decisions I made — change any you disagree with
1. **Kept the 7 class subject notes** (Chemistry, Computation, English, FEyC, History, Lengua, Maths) even though empty. They're current subjects, not speculative folders. Say the word and I'll delete them.
2. **Folder named `C++`** instead of `C++ (learncpp)` — cleaner breadcrumbs; source noted here.
3. **`Learning FRAMEWORK.md` stays in `Self-Improvement/`** rather than a new `Knowledge/Meta-Learning/` folder (avoids a one-note folder).
4. **Neovim notes not merged into a single file** — only moved into one folder, to avoid destroying content. `Drawbacks` were merged because you asked.
5. **Dashboard "Active projects" scoped to `Projects/Coding` + `Projects/School`** so the 22 Ne Obliviscaris chapters don't flood the table. Writing got its own section.
6. **`Next Steps.md` → `Inbox/`** (it's a to-do, not a plan).

## Known broken link (pre-existing, not caused here)
- `Classes/History.md` links to `[[Studying for History Test]]`, which doesn't exist.

## Still needs your hand (when you open in Obsidian)
- Rename done outside Obsidian, so **verify** Settings → Files & Links → Automatically update internal links.
- Check every Dashboard query returns rows.
- Triage `Inbox/`.
