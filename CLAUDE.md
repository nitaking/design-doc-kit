# Instructions for AI working on design docs

Follow these when helping to write, edit, or review design docs in this repository.

## Do not make the author's decisions

Recording the author's decisions and open questions accurately takes priority over completing the design doc. Do not fill in business rules, design decisions, or rationale that cannot be confirmed from the author or the provided materials.

| Allowed | Not allowed |
| --- | --- |
| Ask about the author's explanation, and point out contradictions, gaps, and other possible readings | Answer, in the author's place, a question the author has not answered |
| Offer hypotheses and design options, marked as proposals | Put a proposal into the document as a decision without the author adopting it |
| Organize decisions stated by the author or the materials into prose, diagrams, and tables | Add plausible rationale, or alternatives that were never considered, after the fact |
| Investigate the current behavior from the code | Treat the current behavior as the correct business specification |

You do not need to ask again about what can already be confirmed from the author or the materials. Distinguish what AI proposed from what the author adopted. Do not treat a request to polish the text as approval of a design change.

## How to proceed

1. Check the author's explanation and the provided materials. If there is no initial explanation and the materials do not make up for it, first ask the author about the situation and for concrete examples.
2. If information needed for a decision is missing, ask, and wait for the answer before doing design work that depends on that decision. The number of questions and the form of the answers are not fixed.
3. Leave unanswered parts open. Do not guess in order to fill in blanks or headings.
4. Organize what has been confirmed. Keep facts, guesses, proposals, decisions, and open questions distinct.

Do not write unverified commands or numbers as verified procedures or guaranteed values. Do not confuse a verification plan with its results.

### When the design is left to you

Even when asked to "design it" or told "it's up to you", do not proceed with design docs or models that depend on the author's understanding of the problem or on the author's design decisions while those cannot be confirmed. Ask the author first and wait for the answer. Do not treat a request that leaves the design to you as adoption of individual design options.

Do not present a finished proposal based on unconfirmed assumptions together with your questions. This constraint is the same even if you label it a "proposal" or "tentative".

You may research, organize the issues, and present and compare options to help the author sort out their thinking. Ask the author for the adoption decision, and resume the design work that depends on it after confirming the necessary decisions.

You do not need to ask again about decisions that can already be confirmed from the author or the materials. However, do not equate having the materials with having confirmed the author's decision.

## Structure and prose

- A template is not a fill-in-the-blank specification. Add, change, or merge headings to fit what is being explained.
- Diagram tools and formats are not restricted. Do not create diagrams or comparison tables that the explanation does not need.
- Keep the relationship between condition and result, and between reason and decision. Do not pack separate topics into one sentence.
- Do not add meaningless emphasis or generalities. When polishing, do not change identifiers, specified values, whether something is required, or the strength of an assertion.
- Do not force reference tables into prose. Do not duplicate the same explanation across files.

## Review

When reviewing a design doc, read [REVIEW.md](REVIEW.md) first. Do not infer from the writing style whether AI was used. Check the content of the design and the basis for its decisions.

Do not fix the document by supplying missing decisions on the reviewer's side. Show what is unclear and which part of the design it affects, and return it to the author as a question.

### Review output format

Write findings in the [Conventional Comments](https://conventionalcomments.org/) format. Put the label and subject on the first line, then a blank line, then the basis and the effect on the design. One finding covers one point.

| Finding | Label |
| --- | --- |
| A problem you can show the basis for, such as a contradiction within the document or a mismatch with a confirmed requirement | `issue (blocking)` or `issue (non-blocking)` |
| A point where information is missing and the validity of the design cannot be judged | `question` |
| An optional improvement that is not a defect | `suggestion (non-blocking)` |

In a `question`, write what is unclear and which design decision it affects.

```text
question: The data retention period after account deletion is not stated.

The "Data" section explains only the deletion procedure. Without the retention period, the batch design cannot be judged. Has the period been decided?
```

## Instructions specific to this repository

@local/CLAUDE.md
