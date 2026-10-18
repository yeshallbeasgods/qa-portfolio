# Decision records

A decision record captures one decision: what was going on, what I chose, what else I considered, and what followed from it. They are dated and **never edited after the fact**. If I change my mind, I write a new record that replaces the old one, and the old one stays. That way the reasoning cannot drift out of date, and a reader can see how my thinking changed.

| #    | Date       | Decision                                                                                                                |
| ---- | ---------- | ----------------------------------------------------------------------------------------------------------------------- |
| 0001 | 2026-10-17 | [Each project publishes a status file, and a static hub reads them](0001-status-contract-and-a-client-side-hub.md)      |
| 0002 | 2026-10-13 | [Redact the API key at the client boundary](0002-redact-the-api-key-at-the-client-boundary.md)                          |
| 0003 | 2026-10-10 | [Pin TypeScript to 6.0 until the linter supports 7](0003-pin-typescript-to-6-0.md)                                      |
| 0004 | 2026-10-11 | [Known defects are expected-failure tests that assert the correct behavior](0004-known-defects-as-expected-failures.md) |
| 0005 | 2026-10-17 | [Build reports read-only, publish with the only write-access job](0005-build-reports-read-only-publish-write-only.md)   |

Each record follows the same shape: **Context**, **Decision**, **Alternatives considered**, **Consequences**, and **Evidence**.
