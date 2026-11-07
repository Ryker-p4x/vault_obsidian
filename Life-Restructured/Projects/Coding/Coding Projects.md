# Coding Projects

Index of coding projects. One note per project, each built from [[Project]].

```dataview
TABLE WITHOUT ID
  file.link AS Project,
  default(file.frontmatter.status, "no status") AS Status,
  dateformat(file.mtime, "dd LLL") AS "Edited"
FROM "Projects/Coding"
WHERE file.name != "Coding Projects"
  AND !contains(file.name, "_About")
SORT file.mtime DESC
```
