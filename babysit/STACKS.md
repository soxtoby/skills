# Babysitting a PR stack

Apply the babysit workflow to every tracked PR. Start with the requested PR and discover descendants through native stack metadata or recursively matching each PR's head branch to another PR's base branch. Include only demonstrated stack dependencies.

At startup and on every wake, refresh stack membership using linked-PR metadata and the host's PR data. Add newly discovered layers, link them to this thread, handle existing feedback, and register a watch for each open PR. A watch on the root alone does not cover the stack. Preserve previously tracked PRs through merges, branch deletion, and base retargeting.

Use stack or repository events for new-layer discovery when supported. If available watches do not wake on newly stacked PRs, explain that discovery occurs on subsequent wakes and ask the user to send new PR links to this thread for immediate pickup. Do not claim continuous discovery without an event source.

Address dependency issues from the bottom upward. Work on each PR's own head branch and push fixes there; keep unrelated layers' changes separate. After a lower-layer update, refresh downstream checks and mergeability before declaring those layers ready. Follow the shared approval rules for conflict fixes and behavior changes.

Retain each PR's last inspected head, handled feedback, decisions, and watch state. Use the current watch tool's supported registration flow for all members, then yield; existing watches persist across wakes. When handing control back, stop this thread's watches for every tracked PR and resume the relevant ones when work continues.

A root merge does not end stack babysitting. Finish only after a final discovery pass finds every tracked PR merged or closed, or the user stops the workflow.
