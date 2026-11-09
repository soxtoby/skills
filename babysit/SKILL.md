---
name: babysit
description: Use when watching a pull request or stack for check failures, merge conflicts, or review comments.
---

# Babysit a PR

Invoking this skill authorizes fixing build/test failures, resolving merge conflicts, and handling PR comments under the rules below, including commits, pushes, and comment replies. Merging the PR requires separate authorization.

## 1. Establish current state

Identify the target PR, repository, base, head branch, and head commit. Infer from the current branch when unambiguous; otherwise ask for the PR. Read repository instructions and inspect local changes before editing. Preserve unrelated work.

Fetch current checks and failure logs, mergeability, reviews, inline threads, and general PR comments, including paginated results. Read the surrounding code and discussion before acting. Account for every outstanding failure, conflict, and comment; distinguish resolved or superseded feedback from actionable work. If available, register the PR with `link_pull_request`.

When asked to babysit stacked PRs, including future layers, read [STACKS.md](STACKS.md) and apply its membership, watch, and completion rules throughout this workflow.

## 2. Address outstanding work

### Failed checks and merge conflicts

Diagnose and fix build/test failures, preserving intended behavior and meaningful checks. Resolve conflicts against the current base using repository conventions. If resolution requires an undecided product or design choice, ask about that choice while completing independent work.

For an infrastructure failure, retry when evidence supports a transient cause; report persistent access or infrastructure blockers. A retry is complete only when its result is known.

### Comments

Read and apply [review-feedback](../review-feedback/SKILL.md) for comment dispositions, implementation approval gates, and replies. Publish resulting fixes under step 3.

## 3. Validate and publish

For all changes, including failed-check and conflict fixes, apply the validation, publication gates, and reporting rules in [review-feedback](../review-feedback/SKILL.md). Push to the PR's head branch.

Once all comments are addressed or declined with justification and all resulting fixes are pushed, refresh reviews and request re-review from every reviewer still requesting changes (`CHANGES_REQUESTED`). Confirm each request succeeded or is already pending; retain reviewer and review IDs across wakes to avoid duplicate requests for the same review.

## 4. Keep watching

After each batch, refresh PR state and repeat for new failures, conflicts, and comments. Retain the last inspected head, handled comment IDs, pending decisions, and validation results across wakes to avoid duplicate work or replies.

When T3 Code provides `watch_pull_request`, handle existing feedback first, register any missing watches, and end the turn. Let its events wake the thread; use this watcher instead of polling or starting another watcher. Existing watches persist across wakes. On each wake, inspect fresh state and resume this workflow. Green checks alone do not end babysitting while the PR remains open.

When handing control back for a decision, review, blocker, or stop request, call `unwatch_pull_request` first if watching. Resume watching after the user responds and the resulting work is handled. Use `list_thread_pull_requests` when needed to establish membership or watch ownership, and link any missing target PRs.

Without a persistent watcher, use available bounded monitoring during the active session and state its limits. Report whether monitoring is active, awaiting input, or stopped; claim future monitoring only after it is actually registered.

Finish when the PR merges or closes, or the user stops babysitting; in stack mode, use the completion rule in STACKS.md. Give a brief status covering published fixes, comment dispositions, checks for the current head, and anything awaiting the user.
