---
name: look-for-updates
description: Find new resources to add to the Awesome Radio Astronomy list. Use when the user wants to refresh or grow the list — searches for open, no-auth, programmatically-accessible radio-astronomy data archives, software, papers, telescopes, and learning resources that aren't already listed, verifies them, and stages each as its own pull request following CONTRIBUTING.md.
---

# Look for updates

Find genuinely new, high-quality items for **Awesome Radio Astronomy** and stage them as clean, one-resource-per-PR contributions.

Read `README.md` and `CONTRIBUTING.md` first — the list has a deliberate bias and a strict entry format. Everything below follows from them.

## What qualifies (match the list's bias)

- **Open and accessible** — public data archives, free/open-source software, freely-readable papers/textbooks, telescopes, and learning material.
- **Usable by an independent researcher today** — prefer **no-authentication** and **programmatically accessible** (VO/TAP, REST API, bulk download, pip-installable). A free-account portal is borderline: only include it when it exposes something the catalogue services don't (e.g. raw visibilities), and say so in the entry — mirror how CASDA's "free OPAL account" is described.
- **Real and maintained** — a working URL/DOI (never a placeholder). For software, confirm an OSI license *and* recent activity (commits/releases within ~12 months); skip archived or abandoned repos and repos with **no license file** (no license = not open-source).
- **Not already present** — search `README.md` before proposing anything. A resource already reachable through a listed service (e.g. a catalogue that's just a VizieR table) is a duplicate; skip it.

## How to find candidates

1. Take each section of `README.md` and think about what's missing: new surveys/archives (ALMA, LWA, NANOGrav-style releases, consolidated catalogues), actively-developed pipelines (search, calibration, imaging, RFI, I/O), freely-readable review articles and open textbooks, and open courses/schools.
2. Fan out web searches per section rather than one broad query. Cross-check against `ascl.net`, GitHub topic pages, arXiv reviews, and observatory data-portal pages.
3. For each candidate gather: canonical URL (homepage/repo over a mirror), one-line description, the license + last-activity date (software), and confirmation it's open/no-auth.

## Verify before proposing (do not skip)

- **Link-check every URL.** Run `lychee` (the repo ships `lychee.toml`):
  ```sh
  lychee --config lychee.toml <url> ...
  ```
  Drop anything that doesn't resolve — the list forbids dead links, and CI runs lychee too.
- **Software:** confirm license + recent commits via the GitHub API, e.g.
  `gh api repos/<owner>/<repo> --jq '.license.spdx_id, .pushed_at, .archived'`.
  A `404` on the license endpoint means no license — skip it.

## Write the entry

- Format exactly: `- [Name](https://url) — one line on what it is and why it's useful.` (em dash `—` before the description, single line).
- Place it in the **most specific** section. If several related items have no home, propose a **new subsection** and add a matching entry to the Contents list.
- Order by relevance, then alphabetically when in doubt. If a resource just augments an existing entry (e.g. adding a docs link), **fold it into that line** instead of adding a near-duplicate.

## Stage as pull requests

One resource per PR (small, reviewable). For each accepted candidate, branched off the latest `main`:

1. `git checkout main && git pull && git checkout -b add-<slug>`
2. Apply the single edit to `README.md` (or the fold / new-subsection edit).
3. `git commit`, `git push -u origin add-<slug>`, then `gh pr create` with a body explaining what it is and why it fits the bias.

Because independent PRs that insert near the same anchor line will conflict once one merges, **merge them one at a time**: after each merge, rebuild the next branch on the updated `main` (re-apply its edit — the anchor lines don't move), force-push, then merge. A structural change that must group a few tightly-related entries (a new subsection) is an acceptable exception to one-per-PR — note it in the PR body.

## Report back

Summarize what was added, and — just as important — what was **rejected and why** (duplicate, dead link, no license, auth-walled). Faithful reporting of the rejects is part of the job.
