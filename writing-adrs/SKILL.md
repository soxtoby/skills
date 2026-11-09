---
name: writing-adrs
description: Use when writing or editing an ADR (architecture decision record).
---

# Writing ADRs

Follow the ADR format from the domain-modeling skill's `ADR-FORMAT.md`, and layer these conciseness rules on top so a reviewer can grasp the decision and its reasons in a 30-second skim.

1. Draft the ADR in that format, applying the rules below.
2. Prune every sentence, bullet, and clause the reviewer could lose without losing the decision or its reasons. Finish when the whole ADR fits on one screen and each bullet is one line stating a distinct fact.

## Conciseness rules

- **Title:** State the decision itself, e.g. "Use Postgres for the write model".
- **Summary:** Short plain sentences, one idea each. With more than one reason, state the context and decision in a sentence, then list the reasons as bullets.
- **Optional sections:** One bullet per item. Write considered options as `{Option}: {why not}`.
- **Background:** Link to code, docs, or glossary terms instead of restating them.

## Example

```md
# Ordering and Billing communicate via domain events

Checkout must keep working while Billing or its payment provider is down, so Ordering publishes events instead of calling Billing.

- Events queue during outages, so checkout never waits on payment.
- Ordering depends only on the event contract, not Billing's API.

## Considered Options

- Synchronous HTTP: couples checkout availability to Billing.
- Shared database: blurs ownership of invoice data.

## Consequences

- Invoices are eventually consistent; the UI shows "pending" until Billing confirms.
```
