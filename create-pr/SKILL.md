---
name: create-pr
description: Use when creating a pull request or drafting or editing its title or description.
---

# Create a PR

1. Read the request or linked issue and the full diff from the merge base with the target branch to the PR head (`git diff <target>...<head>`). Establish the intended outcome and its purpose, affected consumers, rollback constraints, and decisions a reviewer might challenge. If the intended outcome or reason for the change is unclear, ask the user and wait for clarification before drafting.
2. Write a short title naming the intended outcome. Compose the body using the rules below, then prune every sentence that adds no distinct information.
3. Create or update the PR when requested; return the draft when only wording was requested. For a published PR, verify the saved title, body, and any image attachments, then return its link.

## PR body

Write the body as short prose, embedded images, and decision bullets, without headings or standalone section labels. Use this order; the goal and final line are required:

- **Goal:** One or two sentences explaining what the PR aims to achieve and why it matters. Describe the problem resolved or capability enabled; keep implementation detail to the decision trade-offs below.
- **Screenshots:** When the outcome is visual and the environment permits, capture the changed behavior and embed the fewest screenshots that demonstrate the goal was achieved. Add a before image only when comparison helps. Use actual captures with image URLs or attachments accessible to reviewers. Omit screenshots when inapplicable or unavailable; report a capture or attachment blocker in the handoff instead.
- **Contentious decisions:** One short bullet per decision a reasonable reviewer might dispute, stating the choice, rationale, and material trade-off. Omit these bullets when there are none.
- **Final line:** `Blast radius: <scope and extent of impact>; revert: <ease and any lasting effects or recovery work>.` Ground both assessments in the change, including affected consumers and persistent state.

Keep the body focused on these four elements. Exclude testing notes, test plans, and validation checklists. Omit placeholders and routine implementation summaries.
