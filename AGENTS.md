# AGENTS.md

Rules for AI agents working in **[project name]**. How the agents are organised overall is in [ORCHESTRATION.md](ORCHESTRATION.md).

## What this repo is

[One paragraph: what the project is, the main parts of the codebase, and where to start reading.]

Checks before a PR: `[your lint, test and build commands]`.

## Who does what

- **The orchestrator** for this repo is **🧭 [Project]**. It keeps the pinned [priorities issue](#) current, assigns work to owners, clears merges and is the only agent that asks [your name] for decisions. It doesn't write product code.
- **Owners** are visible sessions, one per outcome, each in its own git worktree and branch. An owner carries its outcome to done: build, test, PR, merge and follow-up.
- **Routines** run on a schedule and report to the orchestrator.

## Working rules

- **Work in your own worktree and branch.** Never commit on another owner's branch, and never discard someone else's changes.
- **Before editing shared files,** check the open PRs and issues for overlap, and coordinate through the orchestrator.
- **Open a PR early.** Say what changed, why, what you verified and what's still unverified.
- **Independent review:** every substantive PR is reviewed by an agent that didn't write it, before merge. Record the reviewer, the commit reviewed and what happened to each finding in the PR. A PR that skips review says why it's trivial.
- **Merging:** after review and checks, ask the orchestrator for clearance with the PR link and head commit. Merge only the cleared commit. Never push straight to main.
- **Push work in progress often.**

## What needs [your name]

Ask only about the list in [ORCHESTRATION.md › When to ask the human](ORCHESTRATION.md#when-to-ask-the-human): money, customers, production, credentials, irreversible changes, direction, these rules, and genuine uncertainty. For this repo that includes:

- [releases and deploys, e.g. "anything that runs `scripts/release.sh`"];
- [anything touching user data or payments];
- [changes to this file].

The owner presents those PRs in its own thread with a short plain-English summary, puts 🟢 in the thread title, and asks one question: approve and merge, or keep it unmerged.

## Reporting

- Lead with what changed for the user and what you actually observed.
- Distinguish confirmed causes from guesses, and merged from released.
- End every message to [your name] with "Needs you: …" or "Needs you: nothing".
