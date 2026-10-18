# 0001: Each project publishes a status file, and a static hub reads them

**Date:** 2026-10-17 · **Status:** accepted

## Context

I have several test projects, each with its own GitHub Pages site. I wanted one page that shows whether each is healthy right now. GitHub Pages is per repository, and I did not want one repository holding credentials that can read the others.

## Decision

Every project publishes a small `status.json` (schema 1) next to its report. A static hub page fetches those files in the visitor's browser. GitHub Pages serves static files with a header that allows other sites to read them, so no server and no token are needed.

## Alternatives considered

- **A central repository that collects results.** It would need credentials to reach every other repository.
- **The same page copied into every project.** The copies would drift apart.
- **Status badges only.** They show pass or fail, but not counts, age, or links to the report.

## Consequences

- The hub trusts nothing it reads. It validates each file, shows "unavailable" for a bad one, and flags results older than about a day and a half as stale.
- A daily check fails if a project stops publishing valid, fresh data.
- Changes to the format must be additive. An optional `links.trends` field was added without changing the schema version.
- Counting rules are part of the contract: a retried test counts once, by its last attempt.

## Evidence

[The format and how the page uses it](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io/blob/c37bade03e0c353dce73e22bdb754aea4c043a23/README.md), [the script that writes the file](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/scripts/buildStatus.mts), and [the daily validator](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io/blob/c37bade03e0c353dce73e22bdb754aea4c043a23/scripts/validate-status.mjs).
