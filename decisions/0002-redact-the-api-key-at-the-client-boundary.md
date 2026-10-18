# 0002: Redact the API key at the client boundary

**Date:** 2026-10-13 · **Status:** accepted

## Context

The weather service I test accepts its key as part of the URL. The test runner prints request URLs when a call fails, and test reports are published publicly. I checked this with a dummy key against an unresolvable host: the failure message contained the full URL, key included.

## Decision

Every API call goes through one small client. It returns only the status and the body, never the response object. It catches network errors and replaces the key in the message before rethrowing. It attaches a request and response summary to each test with the key replaced, and the API test project has tracing turned off, because traces record URLs.

## Alternatives considered

- **Rely on the CI log masking.** It hides the exact secret value in logs, but not in the published report, and not when the key is embedded in a longer string.
- **Mask only in CI.** A local run would still show the key in a terminal.
- **Attach the original error as the new error's cause.** A lint rule suggested it, but the cause would carry the unredacted message, so the rule is disabled on that one line, with the reason written next to it.

## Consequences

- When the key is missing, API tests are skipped with a clear message, and CI fails loudly on any run that should have it, so a skipped suite cannot pass silently.
- I scanned every generated report, attachment and zipped trace for the key, and for any unredacted `appid=`, and found none. That scan was done by hand, not by a recurring check.

## Evidence

[The client](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/utils/openWeatherClient.ts) and [the environment helper](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/utils/env.ts).
