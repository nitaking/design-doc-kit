# Design Doc

## How to create one

1. Generate the skeleton

    ```shell
    mise run doc:new <slug>
    # e.g. mise run doc:new my-feature
    # -> creates design-docs/YYYY-MM-DD-my-feature/README.md
    ```

2. Edit `README.md`
3. If the explanation reads better split up, copy the template files below into the same directory
4. Open a PR and request a review

> [!NOTE]
> A design doc is stock information. Manage flow information in issues and PR comments.

## Templates

| File | Content | Required |
|---|---|---|
| [`_template/README.md`](_template/README.md) | Background and goal, design, things to discuss | Required |
| [`_template/design.md`](_template/design.md) | Design considerations and decisions | When splitting the explanation |
| [`_template/operations.md`](_template/operations.md) | How to apply the change and respond to failure | When splitting the explanation |
| [`_template/validation.md`](_template/validation.md) | What to confirm and how to verify it | When splitting the explanation |
| [`_template/addons/sudo-modeling/`](_template/addons/sudo-modeling/README.md) | sudo modeling for DDD | Add-on |

The headings and format of the templates are not fixed. Explain, as the author, concrete examples of the current situation and the problem you want to solve, and work through the design in a structure that fits what is being designed.

The viewpoints for self-review and review by others are in [REVIEW.md](../REVIEW.md). You do not need a section for each item. For the constraints when using AI, see [CLAUDE.md](../CLAUDE.md).

## Tips

When you include a D2 diagram, you can attach a link to its source with `<figure>`.

```markdown
<figure>
  <img src="./YYYY-MM-DD-slug/design.png" alt="Design">
  <figcaption>Source: <a href="https://...">figjam</a></figcaption>
</figure>
```
