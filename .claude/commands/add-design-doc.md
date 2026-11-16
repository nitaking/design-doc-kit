# Add Design Doc - Usage: /add-design-doc [taskID] <title> (e.g. PROJ-123 New feature design)

Create a new design doc file under `design-docs/`.

## Arguments

Format of `$ARGUMENTS`: `[taskID] <title>`

Examples:
- `PROJ-123 New feature design`
- `Auth refactoring`

## Steps

1. Parse `$ARGUMENTS`. If the first token has the form of a ticket ID (letters, a hyphen, digits), take it as `taskID` and the rest as `title`. Otherwise take the whole as `title`

2. Decide the directory name:
   - Format: `design-docs/YYYY-MM-DD-<taskID>-<slug>/README.md`. Without a `taskID`, `design-docs/YYYY-MM-DD-<slug>/README.md`
   - The date is today's date (see `currentDate`)
   - The slug is the title in lowercase with spaces replaced by hyphens
   - If a directory with the same name already exists, do not create it. Say so and stop

3. Read the template `design-docs/_template/README.md` and replace `<title>` in the heading with the value of `title`
   - Leave the rest of the guidance (`<!-- -->` comments and `<...>` placeholders) as is, because the author rewrites it

4. Write it to `design-docs/<dir>/README.md`

5. Show the path of the created file and report completion
