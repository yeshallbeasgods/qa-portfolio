# Principles

Six ideas that shaped the projects, each with a link to the code that shows it. The links point to a specific commit (October 2026), so they will keep showing what I mean even after the code moves on. A note on how I work with AI agents is on [its own page](ai-workflow.md).

## 1. One behavior per test, and assertions that wait

A test covers one behavior. Several assertions are fine when they check the same outcome. Assertions retry until they pass or time out, instead of reading a value once or sleeping. Phases of a test are labeled, so a failure says which phase broke.

<!-- Rob: add a line in your own words about why this matters to you. -->

**Evidence:** the [cart tests](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/tests/e2e/cart.spec.ts). Removing an item was one test that checked two behaviors, so it became two tests, each with labeled steps.

**The trade-off:** end-to-end tests are slow, so I do not split every assertion into its own test. Setup is most of the cost. I split only when two checks could fail independently.

## 2. A failure should say what is wrong

A failing test prints where it failed, why, and what it expected against what it received, in plain labels. A missing setting fails at once with its name, not as a timeout ten seconds later. Responses are compared field by field, so a failure names the field.

<!-- Rob: add a line in your own words about why this matters to you. -->

**Evidence:** the [terminal reporter](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/reporters/clearFailureReporter.ts), the [environment helper](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/utils/env.ts), and the [API tests](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/tests/api/openweather.spec.ts).

**The trade-off:** the reporter reads the text of the test runner's error messages, so a runner upgrade can change what it sees. It falls back to the raw message, and the README says to recheck it after upgrades.

## 3. Verify against reality instead of trusting green

Locators come from the running application, not from memory. A test that is expected to fail is checked to fail for the right reason. A pipeline is proven by breaking it on purpose: I pushed a failing test to confirm that a red run still publishes and shows as red, then reverted it.

<!-- Rob: add a line in your own words about why this matters to you. -->

**Evidence:** the [known-defect tests](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/tests/e2e/special-users.spec.ts) and the rules in the [agent file](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/AGENTS.md) about probing the live site first.

**The trade-off:** checking costs time. I spend it where a silent failure is likely (publishing, counting, redaction), not everywhere.

## 4. Test code is production code

Strict types, type-aware linting (including a rule that catches a missing `await`), and a pipeline built with least privilege: the job that builds reports cannot write anything, and the job that publishes runs none of the project's code. Third-party actions are pinned to a commit, and the API key is redacted from errors and attachments.

<!-- Rob: add a line in your own words about why this matters to you. -->

**Evidence:** the [workflow](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/.github/workflows/playwright.yml) and the [API client](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/utils/openWeatherClient.ts). Decisions [2](decisions/0002-redact-the-api-key-at-the-client-boundary.md) and [5](decisions/0005-build-reports-read-only-publish-write-only.md) explain the reasoning.

**The trade-off:** more work up front. I accept it because a test suite runs other people's dependencies, often with real credentials.

## 5. Make quality visible, and keep it honest

Each project publishes a small, versioned status file next to its report. A dashboard reads those files live. A result older than about a day and a half shows as stale, and a daily check fails if a project stops publishing valid data. A failing test run and a broken reporting pipeline are different problems, and they are reported differently.

<!-- Rob: add a line in your own words about why this matters to you. -->

**Evidence:** the [status script](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/scripts/buildStatus.mts), the dashboard's [validator](https://github.com/yeshallbeasgods/yeshallbeasgods.github.io/blob/c37bade03e0c353dce73e22bdb754aea4c043a23/scripts/validate-status.mjs), and [decision 1](decisions/0001-status-contract-and-a-client-side-hub.md).

**The trade-off:** this is infrastructure around the tests, not tests. It pays off once there is more than one project to watch.

## 6. Data-driven, and pin what matters

Cases live in typed arrays and generate one named test each. For live data I assert properties (types, ranges, relationships), not exact values. For deterministic data I assert exact values. Money is compared as numbers within a stated tolerance, never as text.

<!-- Rob: add a line in your own words about why this matters to you. -->

**Evidence:** the [login cases](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/test-data/loginCases.ts) and the [API tests](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/tests/api/openweather.spec.ts).

**The trade-off:** a property check can miss a value that is wrong but plausible. Mocking the network, which makes an API deterministic, is the next step for that.
