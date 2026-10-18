# Playwright + TypeScript

**The question:** can UI tests and API tests share one runner, one set of fixtures and one report you can trust?

## What to look at

- A UI suite against a demo shop (login, cart, checkout, including numeric checks of totals and the site's deliberately broken users) and an API suite against a weather service, both run by the same test runner.
- Page objects handed to tests as fixtures, with no base class and no manager object.
- A failure report that says where, why and expected against received. See [principle 2](../principles.md#2-a-failure-should-say-what-is-wrong).
- A pipeline that lints, runs the UI and API tests as separate jobs, builds an Allure report with a trends dashboard, and publishes it. It also runs nightly.

## A decision worth reading

[Redact the API key at the client boundary](../decisions/0002-redact-the-api-key-at-the-client-boundary.md). The weather service wants its key in the URL, and the test runner prints URLs. This record explains how that is handled.

## What was hard

- **A missing `await` does not fail loudly.** The test races ahead. A lint rule catches it, which is why type-aware linting is worth its setup cost.
- **Types describe shapes but do not check them.** A response interface is erased before the test runs, so the shape tests still have to check the real data.
- **Tool versions are coupled.** TypeScript stays on 6.0 because the linter does not support 7 yet. See [decision 3](../decisions/0003-pin-typescript-to-6-0.md).

## Links

- [Repository](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks) and its [latest results](https://yeshallbeasgods.github.io/universal-cloudless-thousandoaks/)
- [README, including a mapping from the Selenium project](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/README.md)
- [Agent file](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/AGENTS.md)
