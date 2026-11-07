# Dashboard

> Conventions & templates: [[Templates/_About|Templates & conventions]]

## Active projects

```dataview
TABLE WITHOUT ID
  file.link AS Project,
  choice(file.mtime > date(today) - dur(2 days), "working now",
         choice(file.mtime > date(today) - dur(7 days), "recent", "dormant")) AS Signal,
  default(file.frontmatter.status, "no status") AS Status,
  choice(file.frontmatter.due, dateformat(file.frontmatter.due, "dd LLL"), "—") AS "Due",
  dateformat(file.mtime, "dd LLL") AS "Edited"
FROM "Projects/Coding" OR "Projects/School"
WHERE file.size > 0
  AND !contains(file.name, "_About")
  AND file.name != "Coding Projects"
SORT choice(file.frontmatter.status = "done", 1, 0) ASC, file.mtime DESC
```

## Deadlines

```tasks
not done
has due date
path does not include Templates
path does not include Inbox
group by due
sort by due
```

## Per-class now

```dataview
TABLE WITHOUT ID
  file.link AS Class,
  length(filter(file.tasks, (t) => !t.completed AND t.text != "")) AS "Open",
  choice(
    length(filter(file.tasks, (t) => !t.completed AND t.text != "" AND t.due)) > 0,
    dateformat(min(map(filter(file.tasks, (t) => !t.completed AND t.text != "" AND t.due), (t) => t.due)), "dd LLL"),
    "—"
  ) AS "Next due"
FROM "Classes"
WHERE file.size > 0
  AND !contains(file.name, "_About")
SORT file.name ASC
```

## Open tasks

```tasks
not done
path does not include Templates
path does not include Inbox
group by path
sort by path
```

## Recently completed

```tasks
done
path does not include Templates
sort by done reverse
limit 10
```

## Learning tracks
- **[[Progress In learning networking]]** — "Currently in the 7th video at minute 7:03"; course notes in `Knowledge/Programming/Networking/Curso de redes`: 11 notes.
- **[[Knowledge/Books/Clean Code/Clean Code|Clean Code]]** — Clean Code notes.
- **Networking/side projects** — [[HTTP Server|HTTP Server]] and [[C functions for HTTP server|C functions for an HTTP server]].
- **Practice** — [[Projects/Coding/Coding Projects|Coding Projects]] (neetcode problems).

## Writing
- **[[Projects/Ne Obliviscaris/Personajes|Ne Obliviscaris]]** — 22 chapters, plus character and place notes.

## Inbox (unsorted — triage these)

```dataview
TABLE WITHOUT ID file.link AS Item, dateformat(file.mtime, "dd LLL") AS "Added"
FROM "Inbox"
SORT file.mtime DESC
```

## Dormant

```dataview
TABLE
  dateformat(file.mtime, "dd LLL") AS "Last touched"
FROM "Projects/Coding" OR "Projects/School" OR "Classes"
WHERE file.size > 0
  AND !contains(file.name, "_About")
  AND file.mtime < date(today) - dur(7 days)
SORT file.mtime ASC
```

## Needs attention
Notes with no links in or out — connect them or delete them.

```dataview
LIST
FROM "Knowledge" OR "Classes" OR "Projects/Coding" OR "Projects/School"
WHERE file.size > 0
  AND !contains(file.name, "_About")
  AND length(file.inlinks) + length(file.outlinks) = 0
SORT file.mtime ASC
LIMIT 10
```
