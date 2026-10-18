# 0003: Pin TypeScript to 6.0 until the linter supports 7

**Date:** 2026-10-10 · **Status:** accepted

## Context

TypeScript 7 had just been released. The type-aware lint rules I rely on, especially the one that catches a missing `await`, come from typescript-eslint, whose declared support was TypeScript below 6.1.

## Decision

Pin TypeScript to the 6.0 line. Tell the dependency bot to ignore major and minor TypeScript updates until the linter supports the next version, and to leave the Node type definitions on the same major version as the Node I run.

## Alternatives considered

- **Use TypeScript 7 and override the version check.** It works today, but it hides a real incompatibility.
- **Install both, with TypeScript 7 under an alias for the type check and 6 for the linter.** It is possible, but it adds a second compiler and a binary-name clash for a speed gain that does not show at this size.
- **Give up type-aware linting.** That loses the rule I care most about.

## Consequences

- One more thing to revisit: when the linter's supported range includes the next version, remove the ignore rule and upgrade.
- The dependency bot's TypeScript 7 pull request was closed, and the ignore rule has the reason written next to it.

## Evidence

[The dependency bot configuration](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/.github/dependabot.yml), and the "what got harder" list in the [project README](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/README.md).
