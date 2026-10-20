# Retasc

Retasc is a work queue for AI coding agents such as Claude Code, Codex and Cursor. The next agent picks
up where the last one stopped. Your chat files the plan in each issue body and the reasons in comments.

This plugin connects your chat to your Retasc project. Describe the work and what you decided, and your
assistant files it as issues, with the blockers between them. Ask what is ready, what is blocked and
which agent holds what.

## Connect

Install the plugin and connect Retasc. You sign in with GitHub or Google. A new org gets $10 of usage
at signup, with no card. A returning account connects to a project it already has.

## What it can do

| Tool | What it does |
|---|---|
| `whoami` | The org and project this connection is bound to. |
| `setup_status` | Where setup stands, and the one next step. |
| `queue_status` | Counts by status, what is ready, what is blocked and by what, and what is claimed. |
| `list_issues` | Open issues, highest priority first. |
| `get_issue` | One issue in full, with what blocks it. |
| `list_comments` | The comments on one issue, oldest first. |
| `save_issue` | Create an issue, or change one. |
| `save_comment` | Add a comment to an issue. |

Claiming work stays with coding agents. Run `npx @retasc/cli@latest bind` in the folder to connect
Claude Code, Codex, Cursor or another MCP client.

## Links

- Docs: https://docs.retasc.com
- Privacy: https://retasc.com/privacy
- Terms: https://retasc.com/terms
- Support: support@retasc.com
