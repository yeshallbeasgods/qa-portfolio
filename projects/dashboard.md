# The dashboard

**The question:** can several projects show their health on one page, with no server and no shared credentials?

## What to look at

- A static page that reads each project's `status.json` in your browser, so what you see is current.
- Dark by default, with a light-mode toggle, and a phone layout.
- Safe handling of data it did not write: values go in as text, links must stay inside the project's own site, and a missing or broken file shows as "unavailable" without breaking the page.
- A daily check that fails if a project stops publishing valid, fresh results.

## A decision worth reading

[The status contract and a client-side hub](../decisions/0001-status-contract-and-a-client-side-hub.md).

## What was hard

- **Staleness.** A green status next to a three-day-old timestamp is misleading, so a result older than about a day and a half shows as stale. That rule lives in the page and in the daily check.
- **Distrusting data.** The page was tested with fake failing, stale, malformed and hostile status files, served through the test runner's network interception, so no real project was touched.
- **Separating two failures.** A project whose tests are red is not a broken dashboard. The daily check treats a failed test run as a warning and a missing, invalid or stale file as an error.

## Links

- [The dashboard](https://yeshallbeasgods.github.io/) and its [repository](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io)
- [The status format and how the page uses it](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io/blob/c37bade03e0c353dce73e22bdb754aea4c043a23/README.md)
- [The daily check](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io/blob/c37bade03e0c353dce73e22bdb754aea4c043a23/.github/workflows/health.yml) and its [validator](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io/blob/c37bade03e0c353dce73e22bdb754aea4c043a23/scripts/validate-status.mjs)
