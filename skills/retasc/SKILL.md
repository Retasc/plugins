---
name: retasc
description: Retasc is a work queue for AI coding agents. The next agent picks up where the last one stopped. Use it right after Retasc is connected, when the person asks what is in their queue, and when this conversation describes work or decisions to file as issues.
---

# Retasc

Retasc is a work queue for AI coding agents. The next agent to claim an issue picks up where the last
one stopped. Two agents can never hold the same issue. The person's issues live in one Retasc project.
Coding agents such as Claude Code, Codex and Cursor claim those issues one at a time, and each claim
hands the agent the issue and its last checkpoint. In this conversation you file the work and read the
queue. You do not pick work up.

Write what was decided into the issue: the plan in `body`, the reasons as comments. A decision that
stays in this conversation is lost to the agent that does the work.

## Right after you connect

1. Call `setup_status`. It returns one `state` and an `instruction` written for you. Follow the
   instruction, including anything it tells you to say to the person.
2. Name the org and project exactly as `setup_status` or `whoami` returns them. Never invent an org
   name, and never ask the person to make one up.
3. If this conversation already describes work, list the issues you would file. File them with
   `save_issue` once the person agrees.

For a new account, signing in created the first org and project, and the server added $10 of usage
to that org. A returning account connects to a project it already has and gets no second $10.
Nothing else is needed: no card, no CLI install and no API key. Never send a checkout or payment
link. Buying more usage happens in the Retasc Dash.

## The tools on this connection

| Tool | What it does |
|---|---|
| `whoami` | The org and project this connection is bound to. |
| `setup_status` | Where setup stands, and the one next step. |
| `queue_status` | Counts by status, what is ready, what is blocked and by what, and what is claimed. |
| `list_issues` | Open issues, highest priority first. Filter by status, priority, label, author, assignee or deadline. |
| `get_issue` | One issue in full, with what blocks it. |
| `list_comments` | The comments on one issue, oldest first. |
| `save_issue` | Create an issue, or change one. |
| `save_comment` | Add a comment to an issue. |

Every tool works inside the one project this connection is bound to.

## Filing an issue

Call `save_issue` without an `identifier`. Write the title as the outcome a person would check, and put
what, why and how to know it is done in `body`. File one issue per piece of work an agent can finish
on its own.

A create needs four declarations, or the server refuses it:

- `blockedBy`, the ids of open issues this work waits on, or `noDependency`, a one-line reason it
  waits on nothing. File a blocker first so you have its id.
- `work`: `true` for work an agent finishes by changing something, `false` for a container such as
  an epic that groups other issues.
- `changeType`, one of `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`,
  `chore` or `revert`.
- `reviewedSimilar`, only when open issues look like this one. The server refuses the create with
  `DUPLICATE_CHECK_REQUIRED` and names them. Read each with `get_issue`. If one is already this
  work, do not file it again and tell the person which issue covers it. Otherwise call `save_issue`
  again with their ids in `reviewedSimilar`.

Set `priority` (1 Urgent, 2 High, 3 Medium, 4 Low) when the person says how much it matters. When
they name a deadline, set `dueAt` to that moment in epoch milliseconds.

## Changing an issue

Call `save_issue` with the issue's `identifier`. Ask the person before you set `status` to `done` or
`canceled`, because either one closes the issue and releases the work it was blocking. `canceled`
also needs a `cancelReason`. Leave `doing` and `review` to the coding agents working the issue.

## What this connection does not do

- Pick up work. Claiming an issue belongs to a coding agent. If the person asks how the work gets
  done, tell them: "Run `npx @retasc/cli@latest bind` in the folder to connect Claude Code, Codex,
  Cursor or another MCP client."
- Import a backlog from Linear, Jira, Asana, ClickUp or Shortcut. That happens in the Retasc Dash.
- Billing. Usage and top-ups live in the Retasc Dash.

## When a call fails

- The credential is refused: the connection has expired or was removed. Ask the person to connect
  Retasc again in this app.
- The response carries `tellHuman`: pass that sentence to the person as written. Only they can act
  on it.
- A tool "is not available on a chat connection": it belongs to coding agents. Use the tools above.
