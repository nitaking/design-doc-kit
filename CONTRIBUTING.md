# Contributing

## Source and translation

The `ja` branch is the source text. The `main` branch is the English translation and follows `ja`. Send changes to the rules, templates, or README to `ja`; send fixes to the English wording to `main`.

## Change flow

1. For changes to the rules (`AGENTS.md`, `REVIEW.md`) or to the templates, open an issue first and describe the situation where the current text got in the way. Typos, translation fixes, and CI fixes can go straight to a pull request.
2. Create a branch, make the change, and open a pull request. The template asks what changed, why, and how you verified it.
3. CI ([kit.yml](.github/workflows/kit.yml)) creates a repository from the previous version of the kit, then checks that `doc:new` works and that `kit:update` upgrades it to your version without touching `local/` or the design docs.
4. Pull requests are squash-merged. The maintainer reviews every pull request; Copilot code review runs first.

## Writing

- Write rules as what to do, not as prohibitions. One idea per sentence.
- Japanese prose can be checked with `npx textlint <file>`.
- Figures are edited in `assets/*.excalidraw` and exported with `npx @excalidraw/cli render assets/<name>.excalidraw --out assets/<name>.svg`.

## Compatibility

`kit:update` overwrites the files the kit owns. Users only edit `local/` and their design docs under `design-docs/`, so when you rename or move any other file, write the migration steps in the release notes.
