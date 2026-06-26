# Releasing

How the Veripsa team decides what goes in [`CHANGELOG.md`](./CHANGELOG.md).

## The rule of thumb

**An entry is "user-visible" if a Veripsa customer would notice the change
without reading our source code.**

The two places they would notice it are:

1. **The Veripsa check comment on a PR** — wording, the verdict, the
   "Details" link, the suggested land order, the per-path verdict, the
   acknowledge flow.
2. **The dashboard or any read endpoint they hit directly** — hotspot
   surface, structural-lens reader, "Lately" feed, freshness signals.

A change that only shows up in Veripsa's logs, gates, internal metrics, or
the codebase itself does **not** belong in the changelog.

## What goes in

- Wording changes to the check comment that change what we claim.
- New columns, fields, or filters on an existing dashboard or reader.
- New behaviour the customer can trigger (e.g. an hours-scale hotspot
  window, a per-repo scope on a reader).
- Bug fixes that change a verdict the customer would have already seen
  (e.g. a rename that used to break the per-path verdict).
- Newly added entries on the public PR comment (links, per-path
  breakdowns, denominators).
- Security fixes that affect what a customer can observe (e.g. a fix that
  changes what data a tenant sees).

## What stays out

- Internal refactors, file splits, decomposition into helpers.
- Test additions, gate additions, audit closures.
- Database schema changes that don't change a customer-facing field.
- Webhook handler reorganizations that preserve external behaviour.
- Performance work that only shows up in our latency dashboards (we **do**
  list perf work when it visibly shortens time-to-comment on small repos).
- Documentation refreshes in the Core repo itself (private; not customer-
  facing).
- Marketing or article publishes.
- Internal jargon, audit iteration numbers, dogfood-round numbers.

## Phrasing rules

When in doubt, rewrite the entry as **the line you would say to the
customer**, not the line the engineer wrote in the commit message.

Specifically:

- No internal jargon: drop iteration numbers, audit ids, gate numbers,
  dogfood-round numbers, internal-tool names.
- No mechanism: don't describe how a fix works, only what changes from the
  customer's seat.
- No raw counts: never quote a number of files, nodes, or edges. Use
  qualitative wording ("shortens", "no longer", "now exposes").
- No absolute claims: avoid "100%", "always", "never", "guarantees",
  "prevents", "blocks (by itself)". Veripsa is an advisor, not a gate
  enforcer.
- No customer names, logos, quotes, or screenshots — even paraphrased.
- No private support-thread content. If a fix originated from a private
  thread, the entry references the PR number only.

## Cadence

The changelog is updated when the Veripsa team cuts a deploy. We group
entries by **calendar date in the Veripsa team's timezone** so a single
day's worth of merges shows up as one block. We do not ship semantic
version numbers — Veripsa Core is a continuously-deployed GitHub App and
what you actually run is whatever is live on the Veripsa side at webhook
time.

## When in doubt

If you can't decide whether something is user-visible, ask: **would the
customer file an issue if this change weren't documented?** If yes, document
it. If no, skip it.

This file is part of the public changelog repo and is the source of truth
for what "user-visible" means at Veripsa.

Older entries that predate these rules are retroactively rewritten when an
audit catches them — the rules above apply to the file as a whole, not just
the most recent block.
