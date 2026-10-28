# How the agents are organised

**Summary:** Work is split into **lanes**. Each lane has one **orchestrator**, the only agent you talk to about that lane. The orchestrator gives each piece of work to an **owner**, one per outcome, and several owners can work in the same repo at once. Recurring work runs as **routines**. GitHub holds the shared record. You decide only what's actually yours.

## Lanes and orchestrators

- **A lane** is an area or product with its own priorities: an app, marketing, support, your backend. Give each lane its own repo where you can. When a new area needs its own priorities, it gets a new lane; when one winds down, retire it.
- **One orchestrator per lane.** It's a long-lived session and your entry point for anything in that lane.
- **The orchestrator's job:** turn your decisions into owned work, keep the work from colliding, and bring back only the decisions that are truly yours. It's a router and a gatekeeper.
- **The orchestrator doesn't build.** If it writes code, it becomes a hidden extra builder that nobody reviews or owns. It may read code and investigate a problem, but all real work goes to a visible owner.
- **Stay in your lane.** Check every request against what your lane owns. Work for another lane is forwarded there with your words verbatim, in one message, and then dropped. Another agent asking doesn't make work yours.
- **Optional: an orchestrator of orchestrators.** Once you have several lanes, one thin session above them can route new work to the right lane, track what's open across all of them, chase dropped items, and send you one daily list of what needs you. It does no lane work itself.

## Owners

- **One owner per outcome, not per repo.** An outcome is a result worth prioritizing and deciding on its own: a bug or feature that matters to users, a marketing goal, a piece of research or a prototype. Not a file, and not a ticket.
- **Owners are visible sessions.** Each has a title that says what it is, with one purpose emoji in front (✨ feature, 🐛 bug, 🎨 design, 🔍 research or review, ⚙️ tooling, 📝 docs, 🧪 testing, 🚀 release, 🧭 orchestration).
- **No status markers in titles.** Your harness already shows whether a thread is working, idle or waiting. Say what's needed in the conversation and on the issue instead.
- **Each owner works in its own git worktree and branch,** so owners don't step on each other.
- **The mandate.** When you approve an outcome, that approval covers whatever work it takes: investigation, architecture, tests, PRs and fixing what breaks afterwards. The owner doesn't come back to ask about each step. The mandate never covers the things in [When to ask the human](#when-to-ask-the-human).
- **Own it to done.** A merged PR or a green test run isn't the finish line; the result you asked for is. Every open item is in exactly one of three states:
  - *moving:* an owner is working on it now;
  - *needs you:* blocked on your decision, with the exact ask written down and you told once;
  - *done:* checked against the PR, the deploy or the running product.

  "Waiting", "handed off" and "will follow up" are not states. An orchestrator never ends its turn with work nobody is watching.
- **Route by fit, never by availability.** New work goes to the owner whose outcome or code it depends on most, so follow-up changes to a feature usually go back to the owner that built it. Start a fresh owner when the work is clearly separate, when the old owner's context has gone stale, or when it's running on an older model than the work deserves. An idle owner is never a reason.

## Routines

- **Routines handle recurring work** on a schedule: triaging support or crash reports, reviewing analytics, writing a weekly plan.
- **They're autonomous.** You never need to go into their threads.
- **Every run ends by posting a short summary** to its lane's orchestrator, plus any question for you. You read one thread instead of ten.

## GitHub is the shared record

Reading every agent's conversation is slow, costly and out of date the moment it's done. The agents need an external source of truth they can all update in parallel.

- **One issue per outcome,** holding the mandate, the owner, its PRs and the next action. Keep the body current; comments keep the history. Use the [outcome template](templates/outcome-issue.md).
- **One pinned priorities issue per lane,** kept by its orchestrator, mostly for itself: direction, now, next, paused, and what needs you. Readable in about a minute. Use the [priorities template](templates/priorities-issue.md).
- **With several lanes,** you can lift this into one company board: initiatives as parent issues, pieces as sub-issues in each repo, and a status field (Now, Next, Blocked, Needs you, Done). Then "Needs you" is the only decision list.
- **Every change goes through a pull request.** That's where the review, the evidence and the merge decision live.

## Review and merging

- **Independent review.** Every substantive PR is reviewed by an agent that didn't write it: a fresh subagent or another model, given the actual diff, the requirements and the evidence, with room to challenge the claim that it's done. Green CI or the builder's own summary isn't review. Findings are fixed, or rejected with evidence.
- **The same for recommendations.** Before a recommendation reaches you, a fresh agent gets the data but not the conclusion and tries to reach its own. Disagreements are settled first.
- **Merge clearance.** Anything shared goes through the orchestrator: merging to main, deploys, test machines, VMs. An owner with a reviewed PR asks for clearance; the orchestrator checks scope, conflicts with other owners' work and order, then clears **one exact commit**. The owner merges that commit and nothing else. A written clearance on the PR (commit SHA plus "cleared") is the record.
- **Clearance isn't a second review.** The reviewer already checked the code. That keeps the orchestrator fast and keeps quality with the agents closest to the code.
- **Time limits on shared things.** Whoever holds a deploy slot or a shared machine posts progress at least every 30 minutes. After an hour without an update, the waiting agent pings once, then releases it.

## When to ask the human

Ask only about:

1. **Money:** prices, offers, refunds, and any new recurring cost.
2. **Customers:** anything a customer sees, receives or can do.
3. **Production:** deploys and releases of something new.
4. **Credentials:** keys, grants and secrets. Prepare the change; the human runs it.
5. **Irreversible changes:** deleting data, or anything that can't be undone.
6. **Direction:** a feature or design they haven't approved, removing one, or reversing one of their decisions.
7. **The rules:** changes to these files.
8. **Genuine uncertainty:** two reasonable options remain after checking the code and data and getting a blind review, and the wrong pick is costly to undo.

The lane decides everything else, does it, and says so afterwards.

How to ask:

- **One recommendation, never a menu.** A yes-or-no question with your pick, what a yes does, and why, in at most three plain sentences.
- **Batch asks** into one numbered message.
- **One yes covers the plan.** Ask again only for something new from the list above, a higher cost, or a step that wasn't in the plan. Releases to customers, credentials, customer messages and deletions always need their own yes.
- **A no stays a no.** Never route around a refusal or a declined permission.
- **End every message to the human with "Needs you: …"** or "Needs you: nothing".
- **Try it yourself first.** Hand the human only the steps that need their own hands, as one paste-ready block.
- **Their words are the source of truth.** Relay their answers verbatim and log them in one place. A yes given in one thread counts in all of them; nobody asks twice.

## Messages and hand-offs

- **Updates go on GitHub issues.** Send a message only when someone has to act.
- **One batched message per owner,** not a stream. Message limits and pauses can strand work for hours.
- **Watch what you hand off.** Start owners in a way that tells you when they finish, read the result and give the next step.
- **Say what a message replaces,** so crossed messages can't cause flip-flops. Re-read the latest from everyone involved before relaying a decision.
- **Briefs give exact commands,** not intentions.
- **Push work in progress often,** so a crash or restart never strands uncommitted work.

## Reporting

- **Write for the human.** Lead with what changed for the user and what was actually observed. "Created two items in a row and found both in the list" says more than a test count.
- **Say what really happened.** When something breaks or an agent got something wrong, say so plainly. A merged PR doesn't mean a feature is done; observed behavior does.
- **Keep the rules current.** One-off instructions ("stop by midnight tonight") don't become permanent rules. When the human corrects something, fix the shared memory and tell the owners who carry it.
