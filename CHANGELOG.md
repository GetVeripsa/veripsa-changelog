# Changelog

All user-visible changes to Veripsa Core, grouped by the date the change
reached production.

Entries describe behaviour you can observe in the Veripsa check comment,
dashboard, or webhook payload. Internal refactors, audits, gate work, and
infrastructure changes are intentionally omitted — see [`RELEASING.md`](./RELEASING.md)
for the rule of thumb.

Each entry links the public PR by number only. PR numbers refer to the
Veripsa Core repository.

---

## 2026-07-02

No customer-visible changes to Veripsa Core landed on this date. The Core
verdict comment, check behaviour, and read endpoints were unchanged from
2026-06-25.

Customer-visible changes to the broader Veripsa **website and dashboard**
(the `veripsa.com` surface — clearer onboarding and evaluation copy across
the docs guide, how-it-works, and homepage; and a clearer notice on the
signed-in dashboard when GitHub installation details are momentarily
unavailable, so a temporary lookup failure no longer reads as "nothing
installed") are surfaced at
[veripsa.com/whats-new](https://veripsa.com/whats-new).
This changelog covers Veripsa **Core** (the GitHub App and its read
endpoints) only — see [`RELEASING.md`](./RELEASING.md) for the
boundary.

---

## 2026-07-01

No customer-visible changes to Veripsa Core landed on this date. The Core
verdict comment, check behaviour, and read endpoints were unchanged from
2026-06-25.

Customer-visible changes to the broader Veripsa **website and dashboard**
(the `veripsa.com` surface — the standalone example page now redirects into
the dashboard demo so there is one current demo surface; the customers page
refocused on an evaluation path while named stories do not yet exist; the
Trust Center trimmed to state only current, verifiable practice; and more
precise wording on public pages, including the Japanese mirror, about which
pull requests are covered and how a pause reads) are surfaced at
[veripsa.com/whats-new](https://veripsa.com/whats-new).
This changelog covers Veripsa **Core** (the GitHub App and its read
endpoints) only — see [`RELEASING.md`](./RELEASING.md) for the
boundary.

---

## 2026-06-26

No customer-visible changes to Veripsa Core landed on this date. The Core
verdict comment, check behaviour, and read endpoints were unchanged from
2026-06-25.

Customer-visible changes to the broader Veripsa **website and dashboard**
(the `veripsa.com` surface — including a `/try` guided walkthrough,
a `/whats-new` rolling page, a `/procurement` questionnaire response,
a `/trust` page, `/docs` Quick Find, additional `/pricing` FAQ items,
new category landing pages, and Japanese localisation across marketing
and legal pages) are surfaced at
[veripsa.com/whats-new](https://veripsa.com/whats-new).
This changelog covers Veripsa **Core** (the GitHub App and its read
endpoints) only — see [`RELEASING.md`](./RELEASING.md) for the
boundary.

---

## 2026-06-25

### Fixed
- When the Veripsa check fails or warns, the "Details" link on the check now
  takes you to the verdict comment on the PR, not the bare commit page.
  (#458)
- Removed misleading wording on paused PRs that read as if the check was
  "not a block" — the comment now reflects what the verdict actually does.
  (#456)
- Acknowledgement copy no longer reads as a Veripsa approval. Acknowledging a
  warning silences it; it does not endorse the PR. (#459)
- A confusing percentage has been removed from the verdict comment. (#460)
- Softened "likely git conflict" wording in the verdict comment so it doesn't
  overstate certainty. (#457)
- A newly-added file in a PR no longer blanks out the per-path verdict for
  the rest of the PR. (#436, #465)
- The "linked to X through a shared file" line in the verdict comment no
  longer renders with a missing name or an empty parenthesis. (#498)
- The merge-conflict heads-up is no longer attached when the underlying
  signal is uncertain. (#505)
- A coupling that previously read as Clear in a specific edge case now
  reads as Unknown, with a pointer to the file involved. (#506)

### Added
- Honest README, refreshed SECURITY policy, and a published roadmap for the
  Core repo. (#455)
- The verdict comment now flags unresolved git conflict markers left in the
  diff (the `<<<<<<<` / `=======` / `>>>>>>>` lines), as an advisory
  callout. (#468)
- Minimal Unity / C# coverage so a Unity PR is no longer reported as
  "Unknown" — the per-path verdict now shows a real signal on `.cs`
  files. (#472)

### Changed
- Free-tier responsiveness: parallel pre-check reads on PRs and a freshness
  cache on the health endpoint shorten the time from webhook to check
  comment on small repos. (#461)
- Draft PRs are no longer skipped. Veripsa now runs the full analysis on
  drafts, with softened wording so the verdict reads as a scout signal
  rather than a final call. (#474)
- Reliability: a deploy that ships application code ahead of the matching
  database schema is now refused at boot, and the Render deploy step
  auto-applies the schema before the new build goes live, so a
  schema-mismatch deploy can no longer silently break PR processing.
  (#489, #490)
- Reliability: a post-deploy synthetic check now replays a content-free
  webhook against the App and rolls the deploy back if the verdict path
  does not produce output, so a regression that only shows up under real
  traffic is caught and reverted without operator action. (#491)
- Reliability: a windowed failure-ratio signal is now surfaced on a
  dedicated endpoint so the health page can move off green when a
  sustained share of events fail, even when the request queue stays
  shallow. (#501)

---

## 2026-06-23

### Fixed
- A verdict-comment advisory now exposes an honest denominator (the observed
  counts) on the dashboard read endpoint, so you can see how strong the
  signal actually is. (#449)
- Symfony and Laravel projects no longer see false collision warnings
  caused by framework imports. (#447)
- Rust verdicts no longer flag spurious overlap on a test
  target. (#444)
- Default-branch changes no longer leave stale entries from the previous
  default branch. (#446)
- Renaming a file no longer leaves a stale path or a stale alert. (#436, #441)
- Large `.sql` schema dumps are no longer silently skipped on the Veripsa
  side. (#442)
- A rare race on file rename no longer collides on the primary key. (#445)

### Added
- Per-repo scope is now available on the dashboard read endpoint so you can
  ask for one repo's view of an installation. (#449)
- The check's refresh-path title is now deterministic and the raw
  count has been dropped from the customer-facing comment. (#440)

### Changed
- One-command emergency suspend/resume of the Veripsa service, with a
  matching runbook section. (No customer-visible behaviour change unless
  used.) (#451)

---

## 2026-06-22

### Added
- The repo hotspot surface now accepts an **hours-scale** window (1h up to
  90d), not just days. (#414)
- The "Lately" feed now carries the originating PR (change) on each row.
  (#411)
- Land-order suggestions in the verdict comment now **link the colliding
  PR** so reviewers can jump straight to it. (#412)

### Fixed
- Land-order suggestions are deduplicated per PR/branch — overlapping PRs
  no longer print the same line N times.
- Two consecutive pushes from the same author on the same change no longer
  hide the collision warning on a PR. (#419)

---

## 2026-06-21 and earlier

Older changes have not yet been backfilled into this changelog. If you
relied on a Veripsa behaviour that changed before this date and want it
documented, please open a [changelog
request](./.github/ISSUE_TEMPLATE/changelog-request.md).
