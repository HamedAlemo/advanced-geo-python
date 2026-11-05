# Lab: Building a Data Workflow with an AI Agent

In [Working with GenAI Tools](04_working_with_genai_tools.md) you learned how coding agents work: a harness runs a model in a loop, the model reads files like `AGENTS.md`, edits code, runs tests and acts on the results. In lectures 22 to 24 you designed a workflow to calculate a time series of mean NDVI from Landsat for two NEON sites, SJER and HARV. In this lab you bring the two together and build that workflow with an AI coding agent (GitHub Copilot in Agent mode).

The lab is built around one idea: when code is cheap to write, your value lies in the parts an agent cannot do for you. You decide what question to answer and which data fit it, you write the plan, you specify the tests that define what correct means and check that they can fail, you review every change, and you check that the results make scientific sense. The agent writes most of the implementation.

## Who does what

| Step | You | The agent |
|---|---|---|
| Question, data and outputs (lecture 22) | Write them in `AGENTS.md` | Reads them in every session |
| Plan (lecture 23) | Write the pseudocode, with inputs and outputs | Critiques the plan before any code exists |
| Tests (lecture 24) | Write the test plan with expected answers worked out by hand; review the tests; break the code on purpose to check they can fail | Writes the test code from your plan, then runs the tests and works until they pass |
| Implementation | Review every change and commit it | Writes the code, one step at a time |
| Results | Check them against scientific expectations | |
| Code review | Find the problems in code an agent wrote without guidance | |

## Getting started

The lab lives in its own repository: [ndvi-workflow-lab](https://github.com/HamedAlemo/ndvi-workflow-lab). Click "Use this template" to create your own private copy, clone it, and follow `README.md`. You need git, pixi, VS Code and GitHub Copilot (free with the GitHub Student Developer Pack).

```
pixi install
pixi run test
```

## Parts

Each part has its own instructions in the `prompts/` folder of the repository.

| Part | What you do | Time | AI? |
|---|---|---|---|
| 0 | Set up the repository and check that the tests run | 10 min | No |
| 1 | Write `AGENTS.md`: question, data, outputs and workflow | 25 min | No |
| 2 | Ask the agent to critique your plan, then update it | 15 min | Yes, as a reviewer |
| 3 | Write a test plan for one scene, then have the agent write the tests | 30 min | Plan: no. Test code: yes |
| 4 | Build the one-scene functions with the agent, then break them on purpose to check the tests | 25 min | Yes |
| 5 | Build one site, then many sites, and run the workflow | 30 min | Yes |
| 6 | Check the results against what you know about the two sites | 10 min | No |
| 7 | Review a script an agent wrote from a one-line prompt | 20 min | No |
| 8 | Reflect on what worked and what did not | homework | No |

## Habits to practice

- Commit before every agent session. If a session goes badly, `pixi run reset` returns you to your last commit.
- Use a new chat session for each part. Short, focused sessions are easier to review and use fewer credits.
- Read every change with `git diff` before you commit it. If you cannot explain a line, ask the agent to explain it, or change it.
- Never let the agent change your tests to make them pass. If a test is wrong, you fix it.
- Make sure every test can fail. A test whose expected value comes from the same formula as the code checks nothing.
- Passing tests show that the code does what you specified, not that the result is right. Always check the results against what you expect from the science.
- Keep notes as you go in `ai_logs/log.md`, written by you.

## What to submit

Push these to your copy of the repository: `AGENTS.md`, your test plan (`tests/TEST_PLAN.md`) and tests, your code in `ndvi_workflow/`, the csv file and plot in `outputs/`, `ai_logs/log.md`, `REVIEW.md` and `REFLECTION.md`.

<p>&nbsp;</p>
