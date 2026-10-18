# 0004: Known defects are expected-failure tests that assert the correct behavior

**Date:** 2026-10-11 · **Status:** accepted

## Context

The demo shop I test ships users that behave badly on purpose. One user sees the same image for every product, some products cannot be added to the cart for two of the users, and a name field does not keep what is typed. I wanted the suite to acknowledge these without being red or silent.

## Decision

Each defect gets a test that asserts the **correct** behavior and is marked as an expected failure, with the reason in the marker. The test reports as passing while the defect exists. The day the defect is fixed, the test starts failing, which is the signal to remove the marker.

## Alternatives considered

- **Skip the test.** It stops telling me anything.
- **Assert the buggy behavior.** Fixing the bug would then break the suite, and the test would be documenting something wrong.
- **Leave it failing.** Permanent red teaches people to ignore red.

## Consequences

- An expected-failure test can "pass" for the wrong reason, such as a typo in a locator. So I ran a copy with the markers removed and read each real failure to confirm it was the one I meant.
- The terminal report shows these as their own label, separate from ordinary passes.

## Evidence

[The known-defect tests](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/tests/e2e/special-users.spec.ts).
