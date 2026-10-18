# Selenium + Python

**The question:** what does a custom utility library for Selenium look like, and can a project in a different language report its results in the same shape as the others?

## What to look at

- Page objects and a shared base class, a central registry for them, and a shared header component.
- A library of utilities for the hard parts of browser testing: robust clicking, explicit waits and debugging helpers.
- Mobile emulation, and test selection by marker (`smoke`, `mobile`).
- A pipeline that lints, runs the smoke tests, builds an Allure report with a trends dashboard, and publishes it.

## A decision worth reading

[Each project publishes a status file the dashboard reads](../decisions/0001-status-contract-and-a-client-side-hub.md). This repo was the second one to adopt the format, which is what proved it was not specific to the first.

## What was hard

Making a project in another language produce exactly the same status file. This one counts tests from the JUnit XML that pytest writes, where the TypeScript project reads Allure's results. The file has to come out identical, including the rule that a retried test counts once.

## Links

- [Repository](https://github.com/yeshallbeasgods/ephemeral-blazing-berserker) and its [latest results](https://yeshallbeasgods.github.io/ephemeral-blazing-berserker/)
- [Pipeline](https://github.com/yeshallbeasgods/ephemeral-blazing-berserker/blob/bca9113a6546b16d5f6e1d1f378c2d6bfe3087d4/.github/workflows/ci.yml)
- [Agent file](https://github.com/yeshallbeasgods/ephemeral-blazing-berserker/blob/bca9113a6546b16d5f6e1d1f378c2d6bfe3087d4/AGENTS.md)
