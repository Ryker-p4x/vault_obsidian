# Templates & conventions

Apply a template from the core Templates plugin (`Ctrl/Cmd+P` → *Insert template*). Daily Notes should point at `Templates/Daily.md`.

## Frontmatter on every content note
- `type`: `class` | `project` | `book` | `track` | `daily` | `review` | `note`
- `status`: `active` | `done` | `paused` | `someday`

Optional extras: `subject` (classes), `area` (`coding` | `school` | `writing`, projects), `due` (`YYYY-MM-DD`, projects).

## Tasks
Only add tasks that carry meaning — never leave an empty `- [ ]`, it inflates the Dashboard counts. Dates use the Tasks emoji format so Dataview and the Tasks plugin can both read them:

```
- [ ] Read chapter 3 📅 2026-10-20
- [ ] Revise for the History test 📅 2026-10-25
```

- `📅` due · `⏳` scheduled · `🛫` start · `⏫` high priority
- A class or project note can hold **as many tasks as you want**; the Dashboard counts the open ones and shows the next due date automatically.

## Where things go
- Learned something → `Knowledge/`
- Making/doing something → `Projects/` or a subject note in `Classes/`
- A plan or method → `Plans/`
- About your own habits/health → `Self-Improvement/`
- Unsorted → `Inbox/` (triage it)

## Templates available
`Class` · `Project` · `Book` · `Track` · `Daily` · `Weekly Review`

Daily Notes are already wired to `Days/` + `Templates/Daily`.

## Tags (optional, keep the set small)
- Context: `#school` · `#coding` · `#life`
- Kind: `#assignment` · `#exam` · `#dsa` · `#reading` · `#idea`

Tags let any Tasks query filter, e.g. `tag includes #exam`. Don't invent a new tag if an existing one fits.

## Weekly review
Insert `Weekly Review` once a week and file it where you'll re-read it (e.g. `Self-Improvement/`). Its headings mirror the Dashboard.

## Maintenance
The Dashboard's *Needs attention* section lists notes with no links — link them or delete them. Keep `Inbox/` empty.
