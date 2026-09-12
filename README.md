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

The three fit one loop: the goal contract says what done means before code exists, the review panel checks the diff before anyone else sees it, and the usability review looks at what shipped. The state-machine rules the panel's architecture lens checks against are published separately as [CHOP](https://github.com/FortunaTerra-Group/chop).

Copyright 2026 FortunaTerra Technologies Inc. Maintained by Vivek Iyer. Apache-2.0; each plugin carries its own license file.
