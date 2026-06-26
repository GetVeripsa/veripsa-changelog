# veripsa-changelog

User-visible changes to **Veripsa Core** — the GitHub App that flags pre-merge
cross-PR collisions for teams running parallel AI agents.

This repo is a **changelog only**. It does not contain Veripsa's source code,
internal mechanism, or roadmap commitments. Entries describe behaviour you can
observe in the Veripsa check comment, dashboard, or webhook payload — nothing
that would only be visible to someone reading our codebase.

## What's here

- [`CHANGELOG.md`](./CHANGELOG.md) — the entries, grouped by date.
- [`RELEASING.md`](./RELEASING.md) — how we decide what counts as
  "user-visible" and therefore goes in the changelog.
- [`.github/ISSUE_TEMPLATE/changelog-request.md`](./.github/ISSUE_TEMPLATE/changelog-request.md)
  — open an issue if you saw a behaviour change in your repo that isn't
  listed.

## Format

Each release block is a date header followed by **Added / Changed / Fixed**
subsections, similar to [Keep a Changelog](https://keepachangelog.com/):

```
## 2026-06-25

### Fixed
- The check's "Details" link now lands on the verdict comment, not the bare
  commit page. (#458)
```

We do **not** ship semantic version numbers. Veripsa Core is a continuously
deployed GitHub App, not a library; what you actually run is whatever is live
on the Veripsa side at the time of the webhook. We group by **calendar date of
deploy to production** instead.

## How to subscribe

Click **Watch → Releases and discussions** (or **Custom → Releases**) on this
repo. We tag a GitHub Release for each date block so you get one notification
per deploy day, not one per merged PR.

You can also follow the [Veripsa Core
roadmap](../README.md#roadmap) — the changelog tells you what already
shipped; the roadmap tells you what's next.

## What this repo does NOT contain

- **No engine internals.** We do not document how the code graph is built,
  what the resolver does, or how co-change is corroborated. The changelog
  describes what *you*, the user, will notice — not how we made it happen.
- **No roadmap commitments.** Entries are past-tense, "this shipped on date
  X". Future-tense plans live in the Core README's Roadmap section, not here.
- **No customer names, logos, or metrics.** Veripsa does not publish customer
  attribution and does not quote user-reported numbers.
- **No private bug-report content.** If a fix originated from a private
  support thread, the entry references the PR number only.

## Reporting a missing entry

If you observed a behaviour change in Veripsa's check or comments on your
repo and it isn't listed here, please open a [changelog
request](./.github/ISSUE_TEMPLATE/changelog-request.md). We'll either add the
entry or explain why it was an internal-only change.

## License

The contents of this changelog repo are licensed under the [MIT
License](./LICENSE). The Veripsa Core engine itself is **not** open-source
and is **not** distributed under this license — only the changelog text in
this repo is.
