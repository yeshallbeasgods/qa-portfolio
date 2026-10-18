# Start here

**Rob Probst, Software Test Engineer.** This repo explains how my test automation projects are built, and why.

The code lives in the other repos, and the results live on the [live dashboard](https://yeshallbeasgods.github.io/). This is the part in between: the reasoning. If you only have a minute, open the dashboard. If you want to know what I would do on your team, read on.

## How to read this

- **2 minutes:** open the [dashboard](https://yeshallbeasgods.github.io/), then skim the project table below.
- **10 minutes:** read [principles](principles.md), then one [decision record](decisions/README.md).
- **The whole thing:** add [how I work with AI agents](ai-workflow.md) and the rest of the decisions.

## The projects

Each project answers one question. The table says what the question is. To see which projects are publishing live results right now, check the [dashboard](https://yeshallbeasgods.github.io/), which reads each one's results as you load it.

| Project                                                                                                | The question it answers                                                                                               |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| [Playwright + TypeScript](projects/playwright-typescript.md)                                           | Can UI tests and API tests share one runner, one set of fixtures and one report you can trust?                        |
| [Selenium + Python](projects/selenium-python.md)                                                       | What does a custom utility library for Selenium look like, and can it report results in the same shape as the others? |
| [The dashboard](projects/dashboard.md)                                                                 | Can several projects show their health on one page, with no server and no shared credentials?                         |
| [Four smaller repos](projects/smaller-repos.md) (Playwright + Java, Cypress, Appium, Python API suite) | What does each tool look like at small scale?                                                                         |

## What this repo is not

It does not copy the other repos' READMEs or agent files. Those change often, and a copy would be wrong within a week. Instead, this repo links to the live files, and to a tagged version where it matters. What lasts is here: the principles, the reasoning, and dated records of decisions.

## Also

- [Live dashboard](https://yeshallbeasgods.github.io/)
- [LinkedIn](https://www.linkedin.com/in/robert-probst-737364b8)
- [GitHub profile](https://github.com/yeshallbeasgods)
