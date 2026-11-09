---
name: review-feedback
description: Use when evaluating and addressing findings from code reviews or PR comments.
---

# Review feedback

Apply these rules within the calling workflow's scope and existing authorization. That workflow determines when to publish; this skill defines how to handle findings and the gates for publishing fixes.

## Evaluate and address

Evaluate each human or automated finding against the code, intended outcome, and repository conventions. Read the surrounding implementation and discussion; distinguish actionable concerns from superseded feedback. Choose one disposition per concern:

- **Not worthwhile:** leave the code unchanged and give a brief, concrete justification.
- **Meaningful behavior change:** explain the proposed before/after behavior and recommendation; ask whether to make the change before implementing it. This gate applies even to a one-line edit.
- **Large code change:** explain scope and recommendation; ask whether to make the change before implementing it.
- **Purely mechanical or small and worthwhile:** implement it and report the change briefly after publication.

Judge size by conceptual scope and review burden, not line or file count. A consistent internal rename across many files can be mechanical; a public API rename can meaningfully change behavior. Investigate uncertain behavior or scope, then ask if it remains unresolved. Combine overlapping approval questions and honor explicit authorization already given.

Assume the operator has not read the review comments. When asking for a decision, summarize the concern, relevant current behavior, your assessment, recommended response or change, and material trade-offs. Include a comment link when available, but make the question answerable without opening it.

Track every concern as addressed, declined with justification, or awaiting the user's decision. Revisit it only when new evidence or feedback changes the disposition. Continue independent authorized work while a decision is pending.

## Validate and publish fixes

Run checks appropriate to the change, including the failing build/test when applicable. Inspect the final diff for unintended changes. Refresh the remote head and relevant discussion before publishing; reconcile concurrent updates first.

- **Small or mechanical changes:** commit only the relevant changes and push to the intended branch when the calling workflow reaches publication.
- **Large changes, including failure or conflict fixes:** finish implementation and validation locally, then present the diff and results for user review before pushing. Approval to implement a finding is distinct from approval to publish the resulting large change; honor explicit authorization already given for either stage.

Keep changes awaiting review separate from changes authorized for push. A local fix or failed push is not a published fix; report its actual state. When a PR exists, check CI for the pushed commit, since results from an earlier head do not validate it.

## Report dispositions

When referring to the human operating you, use "my meat-puppet".

For findings from local or delegated reviews, report dispositions to the caller. For PR comments, reply on the triggering comment: explain declined findings, and acknowledge fixes only after a successful push.

Prefix every response to a PR comment with `🤖 `, including acknowledgments, explanations, and justifications for declining changes. Keep fix replies brief: "🤖 Fixed", "🤖 Done", "🤖 Renamed as requested", or a short explanation when needed.
