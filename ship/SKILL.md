---
name: ship
description: Use when taking a branch through review, PR creation, and a babysitting handoff.
---

# Ship

1. Run two independent, read-only `delegate_task` reviews in parallel: the latest Astra and latest Opus, both at `xhigh`. Both review the same branch head and the full diff from its merge base with the target branch (`git diff <target>...<head>`).
2. Once both reviews finish, apply [review-feedback](../review-feedback/SKILL.md) to their findings. Proceed when every finding is addressed or declined with justification.
3. Push the branch and create a PR using [create-pr](../create-pr/SKILL.md).
4. Resolve the babysit environment from the label in the `SHIP_BABYSIT_ENVIRONMENT` environment variable: the current environment when the label matches `t3_environment_read`, otherwise the reachable `t3_environment_links` entry with that label. When the variable is unset or no reachable environment matches, report that and ask the user where to launch.
5. Use `t3_thread_launch`, passing the resolved `environmentId` and that environment's project for this repository, to start a new thread in a new worktree with the PR branch checked out at the published head, with load balancing when available. Tell the thread to use [babysit](../babysit/SKILL.md) for this PR and every PR stacked onto it, including future layers.
