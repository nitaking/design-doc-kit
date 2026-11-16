# design-doc-kit

A foundation for repositories where design docs are written and reviewed. It assumes AI must not make the author's decisions.

[日本語](https://github.com/nitaking/design-doc-kit/tree/ja)

![When AI writes, everything looks decided. When AI asks, you can tell what is decided from what is open](assets/overview.svg)

## Why this exists

### When design docs were managed in Notion

- The diagrams Notion renders are Mermaid
  - Commenting on part of a diagram is awkward
- When the commented part is changed, the comment is lost
- Diagrams other than Mermaid are hard to render
- Version control is hard

We wanted to exchange proposals, comments, and revisions the way pull requests allow, and to merge into develop.

### After adopting Git

- Applied as a submodule, it became easier to let AI coding agents run on their own across multiple repositories
- In reviews too, agents can be used with consistent specifications and context
- For people as well, it became easier to reflect the design
- It is especially effective for designs with clear inputs and outputs, such as databases and APIs

### What became a problem afterwards

- Working out a design by talking it through with AI became easier. On the other hand, AI gets ahead of the author's thinking, so the design becoming shallow turned into a risk
- With little design experience, or with experience but no time to think, it is hard to get out of the bias of a proposal once you have seen it
- Design is where understanding is needed most, and AI output that the eyes slide over gets in the way of understanding

### Motivation

After these experiences, this kit sets up a format in which people can immerse themselves in thinking, and AI does not design and only accompanies.

The constraints for AI are in [CLAUDE.md](CLAUDE.md), and the review viewpoints are in [REVIEW.md](REVIEW.md).

## What is included

![Files owned by the kit and files owned by your repository](assets/included.svg)

The Japanese edition on the [`ja` branch](https://github.com/nitaking/design-doc-kit/tree/ja) is the original text. It also includes textlint rules for Japanese prose.

## Usage

Create a repository from "Use this template" on GitHub. [mise](https://mise.jdx.dev/) is required.

```shell
mise install
mise run doc:new <slug>     # creates design-docs/YYYY-MM-DD-<slug>/README.md
mise run d2:png             # converts changed .d2 files to PNG
```

For how to write a design doc, see [design-docs/README.md](design-docs/README.md).

## Repository-specific settings

Do not edit the files this kit owns. Write repository-specific content in `local/`. This avoids conflicts when you pull updates from the kit.

| What to write | Where |
| --- | --- |
| Instructions for AI specific to the repository | [local/CLAUDE.md](local/CLAUDE.md) |
| Review viewpoints specific to the repository | [local/REVIEW.md](local/REVIEW.md) |
| Your own README | `.github/README.md` |

## Pulling updates

```shell
git remote add upstream https://github.com/nitaking/design-doc-kit.git   # first time only
mise run kit:update        # merges upstream/main
```

## License

- Configuration files and task definitions: [MIT](LICENSE)
- Text of the rules and templates (Markdown): [CC BY 4.0](LICENSE-CC-BY-4.0)
