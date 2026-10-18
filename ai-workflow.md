# How I work with AI agents

I use an AI coding agent (Claude Code) on these projects. The short version: **I decide, the agent executes under written constraints, and everything it claims gets verified.**

<!-- Rob: rewrite this in your own voice. Keep the examples; they are real. -->

## The rules are written down

Each project has an `AGENTS.md` file that the agent reads at the start of a session. It is short on purpose. A line belongs there only if the code cannot tell the agent the same thing. Here is what each section is for, and why it exists.

| Section                            | What it holds                                                                               | Why it exists                                                     |
| ---------------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Commands**                       | Only commands that exist and run, plus "do not invent others"                               | An agent will confidently run a command that does not exist       |
| **Conventions**                    | Rules that tooling does not enforce: how to import, how to tag, how to compare money        | Lint already catches the rest, so listing it would only add noise |
| **Secrets**                        | Where the key lives, how it is redacted, what never to log or attach                        | Reports are public, so a leak here is a real leak                 |
| **Writing page objects and specs** | How to find locators and what to check before committing a new one                          | This is where the agent's guesses cost the most                   |
| **Working agreement**              | Plan first, small steps, ask before adding a dependency or touching CI, report real results | It keeps me in the loop and makes the agent's claims checkable    |
| **Debugging loop**                 | How to read a failure locally and in CI                                                     | A shared routine means the agent and I look at the same evidence  |

The live files: [Playwright + TypeScript](https://github.com/yeshallbeasgods/universal-cloudless-thousandoaks/blob/8bb7c39e37f5d8fdca424230ea728d2f890c3fc4/AGENTS.md) and [Selenium + Python](https://github.com/yeshallbeasgods/ephemeral-blazing-berserker/blob/bca9113a6546b16d5f6e1d1f378c2d6bfe3087d4/AGENTS.md). I link to them instead of copying them, because they keep changing.

## What I do not hand over

I was learning Playwright and TypeScript while building these, so the concept-heavy first pieces are mine: the first page object, the fixtures file, and the first spec. The agent reviewed them and explained what was wrong. It wrote the setup, the configuration and the repetitive parts. The agent commits or pushes only when I ask.

## Where the agent was wrong, and how it was caught

This is the part I think matters most. The agent makes mistakes, and the system around it is what catches them.

- **It read the wrong page.** While probing the checkout pages for element IDs, the agent's script waited for the URL to change and then read the page. The site changes its URL before it renders, so the script read the previous page's content. I found it because the output did not match the page. The fix, "wait for something unique to the new page, never the URL", is now a rule in `AGENTS.md`.
- **It counted a test three times.** The script that summarizes results counted every retry as a separate test, so one failing test would have shown as three failures. It was caught while planning a deliberate failure to test the pipeline, and fixed after checking against the real artifacts from an earlier failed run. The fix has its own tests.
- **It applied nothing, silently.** A script meant to apply security settings to eight repos ran once against a single, invalid name because of how the shell splits words, and changed nothing. The output looked odd, so I checked it, and the fix was to run it again and then re-audit all eight repos to confirm the settings were actually in place.
- **A mistake that types and lint could not catch.** A test I wrote compiled and linted cleanly, then failed at runtime because I had put an assertion where a value belonged. The new failure report pointed at the exact field, which is what the report is for. The lesson: always run the test.
- **A green test that might be green for the wrong reason.** Tests that are expected to fail pass when they fail, including when they fail for a typo. I ran a copy with the expected-failure markers removed and read each real failure to confirm it was the failure I meant.

## Guardrails on the tools themselves

- The agent never reads the `.env` file, and the rule is written in `AGENTS.md`.
- A permission rule stops it reading the folder where the GitHub command-line tool stores its login token. That rule only covers the agent's file tools, so I also rotate the token and log out when I am not using it.
- Anything the agent produces that affects security, like workflow permissions or settings on a repository, gets read by me before it runs, and I check the result afterward.

## What I would tell a team adopting this

Write the rules down, keep them short, and make the agent report real results. Then treat every "done" as a claim to check, because that is what catches the mistakes above.
