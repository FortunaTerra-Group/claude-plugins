# FortunaTerra Claude Code plugins

A plugin marketplace for FortunaTerra's public Claude Code skills. Each skill lives in its own repository; this repository only holds the manifest that lets Claude Code find them.

```bash
claude plugin marketplace add FortunaTerra-Group/claude-plugins
claude plugin install multi-persona-review-panel@fortunaterra
claude plugin install usability-heuristic-review@fortunaterra
claude plugin install governed-build-loop@fortunaterra
```

| Plugin | What it does | Repository |
|---|---|---|
| `multi-persona-review-panel` | Independent reviewer lenses on your diff before the PR, one verdict per lens | [multi-persona-review-panel-skill](https://github.com/FortunaTerra-Group/multi-persona-review-panel-skill) |
| `usability-heuristic-review` | Heuristic evaluation of a shipped UI surface, severity on every finding | [usability-heuristic-review-skill](https://github.com/FortunaTerra-Group/usability-heuristic-review-skill) |
| `governed-build-loop` | A goal contract written before code, with an independent review of the contract | [goal-contract](https://github.com/FortunaTerra-Group/goal-contract) |

## Worked example

Add the marketplace, install one plugin from it, and check that it is there:

```bash
claude plugin marketplace add FortunaTerra-Group/claude-plugins
claude plugin install multi-persona-review-panel@fortunaterra
claude plugin list
```

Inside a Claude Code session the same steps are `/plugin marketplace add FortunaTerra-Group/claude-plugins` and `/plugin install multi-persona-review-panel@fortunaterra`.

Then, on a branch with a non-trivial change and before you open the PR, invoke the skill. Plugin skills are namespaced by plugin name, so this one is `/multi-persona-review-panel:multi-persona-review-panel`; asking Claude to "run the review panel on this branch" also matches the skill's description.

The skill tells the agent to take the whole diff against the base branch, start one independent reviewer per lens (architecture, security, quality, performance), and return findings with file and line plus one verdict per lens: SIGN, SIGN-WITH-CHANGE or BLOCK. The plugin's [`examples/example-run.md`](https://github.com/FortunaTerra-Group/multi-persona-review-panel-skill/blob/main/examples/example-run.md) is a recorded run on a sample rate-limiting change in a demo repository. In that run all four lenses returned BLOCK on the first pass, and three root causes were found by all four lenses independently. After the author folded the findings and reran the panel, the second run still had one BLOCK (on a test, not on code) and the third run returned four SIGN-WITH-CHANGE converging on one remaining item. The example also notes that panels converge but should not be expected to reach four bare SIGNs.

The other two plugins work the same way and each has its own worked example:

- `governed-build-loop`: invoke it before starting a feature; it asks for a four-section contract (GOAL, CONTEXT, DECOMPOSITION, DO-NOT) and an independent read of that contract before any code. See its [example run](https://github.com/FortunaTerra-Group/goal-contract/blob/main/plugin/examples/example-run.md).
- `usability-heuristic-review`: invoke it with a shipped UI surface and the product's persona documentation; it returns a findings report with a severity on every finding. See its [example run](https://github.com/FortunaTerra-Group/usability-heuristic-review-skill/blob/main/examples/example-run.md).

Each plugin README has a section, "What this plugin runs and sends", stating what the plugin does on your machine.

The three fit one loop: the goal contract says what done means before code exists, the review panel checks the diff before anyone else sees it, and the usability review looks at what shipped. The state-machine rules the panel's architecture lens checks against are published separately as [CHOP](https://github.com/FortunaTerra-Group/chop).

Copyright 2026 FortunaTerra Technologies Inc. Maintained by Vivek Iyer. Apache-2.0; each plugin carries its own license file.
