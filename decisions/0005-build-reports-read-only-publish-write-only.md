# 0005: Build reports read-only, publish with the only write-access job

**Date:** 2026-10-17 · **Status:** accepted

## Context

Publishing a report to GitHub Pages needs permission to write to the repository. Building the report needs the project's dependencies installed, and installing dependencies runs code written by other people.

## Decision

Split the work into two jobs. The **report** job installs dependencies and builds the report with read-only access. The **publish** job has write access, runs none of the project's code, and only moves the finished files into place. Checkouts do not keep the access token on disk. The one third-party action that publishes is pinned to a full commit, because it runs with write access and a version tag can be moved.

## Alternatives considered

- **One job that builds and publishes.** A compromised dependency could then use a token that can write to the repository.

## Consequences

- One extra job, and a handoff of the built site between the two jobs.
- Pinned actions need updating. The dependency bot keeps commit-pinned actions current, so the cost is review time, not manual tracking.
- Publishing is limited to the main branch and the nightly run, so pull requests build the report but never publish it.

## Evidence

[The workflow](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/.github/workflows/playwright.yml).
