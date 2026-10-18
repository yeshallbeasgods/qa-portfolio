# Start here

**Rob Probst, Software Test Engineer.** This repo explains how my test automation projects are built, and why.

Code lives in the other repos, and the results live on the [live dashboard](https://yeshallbeasgods.github.io/). This is the part explains my reasoning and test philosophy out loud. If you only have a minute, then open the dashboard. If you want to know what I would do on your team, then read on.

## How to read this

- **2 minutes:** Open the [dashboard](https://yeshallbeasgods.github.io/), then skim the project table below.
- **10 minutes:** Read [principles](principles.md), then one [decision record](decisions/README.md).
- **The whole thing:** Add [how I work with AI agents](ai-workflow.md) and the rest of the decisions.

## The projects

Each project focuses on one theme and the table below says what the guiding question is. To see which projects are publishing live results right now, check the [dashboard](https://yeshallbeasgods.github.io/), which reads each one's results as you load it.

| Project                                                                                                | The question it answers                                                                                               |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| [Playwright + TypeScript](projects/playwright-typescript.md)                                           | Can UI tests and API tests share one runner, one set of fixtures and one report you can trust?                        |
| [Selenium + Python](projects/selenium-python.md)                                                       | What does a custom utility library for Selenium look like, and can it report results in the same shape as the others? |
| [The dashboard](projects/dashboard.md)                                                                 | Can several projects show their health on one page, with no server and no shared credentials?                         |
| [Four smaller repos](projects/smaller-repos.md) (Playwright + Java, Cypress, Appium, Python API suite) | What does each tool look like at small scale?                                                                         |

## What this repo is not

It does not copy the other repos' READMEs or agent files because those change often, and a copy would be wrong within a week. Instead, this repo links to the live files or to tagged versions. That way, the principles, reasoning, and dated records of decisions can be viewed here.

## Also

- [Live dashboard](https://yeshallbeasgods.github.io/)
- [LinkedIn](https://www.linkedin.com/in/robert-probst-737364b8)
- [GitHub profile](https://github.com/yeshallbeasgods)
