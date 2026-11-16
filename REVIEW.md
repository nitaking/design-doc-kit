# Reviewing design docs

Use this for the author's self-review and for review by others. Do not judge from the writing style whether AI was used. Check the content of the design and the basis for its decisions.

This does not require an answer to every item or a dedicated section for each. Check the viewpoints relevant to the change, and reflect in the document only what readers need explained. Also check points not listed here, depending on what is being designed.

Viewpoints specific to this repository are in [local/REVIEW.md](local/REVIEW.md).

## Connection between the problem and the design

- Is the problem to be solved explained together with the business or usage context it applies to?
- Is the rationale based on this problem and its constraints, not on general advantages?
- Can confirmed facts, guesses, proposals, decisions, and open questions be told apart?
- Can the basis for important decisions be traced from the document or its references?

## Checks depending on the change

| Viewpoint | What to check |
| --- | --- |
| External APIs | Are token expiry and refresh, error handling, and retries considered? Check the failures that occur with the API in use, such as 401 and 429. |
| Data | What is recorded, and which states and history need to be explainable? Is the handling of data decided, including retention and deletion after account deletion? |
| Permissions | Who uses it, and which resources can they read, save, and change? Do admin screens and derived resources also have the restrictions they need? |
| Input and secrets | Are type, length, and required conditions validated? Is the storage location for credential files, keys, and secrets appropriate? |
| Compatibility | How are existing users and integrations affected? If the specification changes, can the migration be explained? |
| Applying and recovering from the change | Can the order of work, the conditions for moving to the next step, and the response to failure be followed? Check what is needed to judge, such as data migration, downtime, and whether and how quickly it can be rolled back. |
| Staged rollout and retirement | Can the targeting conditions, such as feature flags, be explained? If an old feature or flag is retired, check the timing and preconditions. |
| Verification and evaluation | By what method and result will the concerns of this change be checked? Is the evaluation of the feature limited to collecting logs? |
| Checks after release | What is checked and when, how is an anomaly judged, and who is told? If logs or metrics are used, is the information needed for investigation available? |

## Readability of the explanation

- Can you tell who does what under which conditions? Has splitting sentences changed what a condition or reason applies to?
- Can you follow the options being compared, and how operations map to results? Do the diagrams, tables, and prose fit the content?
- Is the explanation of one process scattered only to match the template's categories?
- Are there leftover fill-in examples or duplicated explanations? Is an important point missing because it was outside the template's items?

## How to return findings

When you find something unclear, show the location, what cannot be judged, and the effect on the design, and ask the author. When you offer an improvement, keep it distinct from a decision.

Deal with the content of the document and its effects, not the author's ability or attitude. State clearly the problems you can show the basis for, and ask about what you cannot judge. Confirmed problems do not need to be turned into roundabout questions.

Do not complete the design on the reviewer's side by supplying business rules or rationale. For constraints on AI review, follow [AGENTS.md](AGENTS.md).

## Guidelines referred to

- [Google Engineering Practices](https://google.github.io/eng-practices/review/reviewer/comments.html) recommends explaining the reason for a comment and distinguishing required changes from optional suggestions. It says the reviewer does not need to design the whole solution.
- [Conventional Comments](https://conventionalcomments.org/) proposes a format that shows the intent of a comment with a label and adds the reason or next step to a short subject. It uses questions for uncertain problems.
- [GitLab Code Review Guidelines](https://docs.gitlab.com/development/code_review/#reviewing-a-merge-request) recommends using Conventional Comments and marking optional suggestions.
- [Code Review Skill](https://github.com/awesome-skills/code-review-skill/blob/main/SKILL.md) and its [PR Review Template](https://github.com/awesome-skills/code-review-skill/blob/main/assets/pr-review-template.md) show a structure that conveys the scope checked, specific good points, important concerns, and the conclusion of the review. This document adopts the idea of briefly stating the scope checked and the next step, and makes good points optional. It does not adopt fixed checklists or approve/reject verdicts as they are.
