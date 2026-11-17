---
name: writing-commit-messages
description: Write Git commit messages when drafting a message, creating a commit, or rewording existing commits.
---

# Writing commit messages

1. Read the diff for the selected change. Use the supplied patch or specified commit/range; otherwise use the staged diff. Account for every meaningful change before choosing the primary user-visible or developer-visible outcome. If the selection is empty, report that there is no change to describe.
2. Apply the user's instructions and repository guidance. Consult recent commit subjects to match the local style.
3. Draft and check the message against the rules below. Finish when its claims match the selected diff, every body line tells the reader something the diff alone does not, and its format satisfies the caller.

## Message rules

- **Subject:** State the primary change in the imperative, at most 72 characters including any prefix, with no trailing period.
- **Body:** Carry the *why*: the motivation, a consequence a reviewer would not see in the diff, or a change unrelated to the subject. The diff is the record of *what*; leave the helpers, overloads, and mechanics to it. Omit the body when the subject is sufficient; otherwise use one short bullet per point.
- **Output:** Return only the message, with a blank line between subject and body. Follow an explicitly requested output format instead when provided.
