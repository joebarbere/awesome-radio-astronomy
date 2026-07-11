# Contributing

Thanks for helping grow **Awesome Radio Astronomy**. A few guidelines keep the list useful and consistent.

## What belongs here

- **Open and accessible** resources: public data archives, free/open-source software, freely-readable papers and textbooks, telescopes and observatories, and learning material.
- Things an independent researcher or student can actually **use** — bias toward no-authentication, programmatically accessible, and well-maintained resources.
- Each entry must be **real and verifiable**: a working URL/DOI, not a placeholder.

## How to add an entry

1. One resource per pull request (small PRs are easy to review).
2. Put it in the **most specific** section. If no section fits, propose a new one.
3. Format: `- [Name](https://url) — one line on what it is and why it's useful.`
4. Keep the description to a single line; use an em dash (`—`) before it.
5. Order within a section by relevance, then alphabetically when in doubt.
6. Prefer a project's canonical homepage or repository over a mirror.

## What to avoid

- Dead links, paywalled-only resources, or abandoned/unmaintained tools.
- Duplicates — search the list first.
- Self-promotion without genuine, broad usefulness.

## Checks

Run a quick link check before opening your PR. CI verifies links automatically with [lychee](https://github.com/lycheeverse/lychee) (see `.github/workflows/links.yml`); reproduce it locally with the shared config:

```sh
lychee --config lychee.toml README.md
```

By contributing you agree to release your contribution under [CC0 1.0](LICENSE).
