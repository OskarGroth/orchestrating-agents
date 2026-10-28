# Orchestrating agents

The rules I use to run many AI coding agents in parallel as a solo developer, generalized so you can adapt them to your own projects.

The short version: you talk to one **orchestrator** per area of work. It hands each piece of work to its own **owner** agent, keeps them out of each other's way, and only brings you the decisions that are actually yours. GitHub issues and pull requests are how the agents keep track of everything.

## What's here

| File | What it's for |
|---|---|
| [ORCHESTRATION.md](ORCHESTRATION.md) | How the whole system fits together: lanes, orchestrators, owners, routines, and when to ask you. Keep one copy where every session can read it. |
| [AGENTS.md](AGENTS.md) | A drop-in rules file for a single repo with an orchestrator. Copy it into the repo and fill in the bracketed parts. |
| [templates/priorities-issue.md](templates/priorities-issue.md) | The pinned issue an orchestrator uses to keep track of its lane. |
| [templates/outcome-issue.md](templates/outcome-issue.md) | One issue per piece of work: the mandate, the owner and the next step. |
| [templates/pull_request_template.md](templates/pull_request_template.md) | A PR description written for you, not for the agents. |

## How to start

1. Pick one project and start a single orchestrator session in it. Give it [ORCHESTRATION.md](ORCHESTRATION.md) and ask it to adopt the rules in that repo's `AGENTS.md`.
2. Let it run one real piece of work end to end before adding more lanes. You'll find out quickly which rules you actually need.
3. Change the rules when something breaks. Rules that come from real failures stick; rules copied from somewhere else mostly get in the way.

## Assumptions

- Each agent runs in its own session that you can see, and sessions can message each other. I use Claude Code, where an orchestrator can start owner sessions and message them directly.
- Every repo is on GitHub, with issues and pull requests turned on.
- Agents can create git worktrees, so several of them can work in the same repo at once.

None of it depends on a particular model, but the orchestrator role needs a strong one. In my experience, how well a model can coordinate other agents matters more than how well it codes.

## License

MIT (see [LICENSE](LICENSE)). Copy, change and use it however you like.
