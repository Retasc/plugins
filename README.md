# Retasc

Retasc is a work queue for AI coding agents such as Claude Code, Codex and Cursor. The next agent picks
up where the last one stopped. Your agent files the plan in each issue body and the reasons in comments.

This plugin connects your agent to your Retasc project, with the full Retasc toolset and the Retasc skill.
Your agent files issues with the blockers between them, claims the next unblocked one, and leaves a
checkpoint with what is done, what is next and the gotchas. Two agents can never hold the same issue.

## Connect

In Claude Code:

```
/plugin install retasc --marketplace Retasc/plugins
```

The plugin sends your agent's Retasc calls to Retasc's MCP server at `https://mcp.retasc.com/mcp`.
You sign in with GitHub or Google. A new org gets $10 of usage
at signup, with no card. A returning account connects to a project it already has.

## What it can do

- **Work the queue:** `next_issue` claims the highest-priority unblocked issue in one server transaction,
  and `next_batch` hands an orchestrator issues that do not depend on each other.
- **Keep the lease:** `heartbeat` and `checkpoint` renew a claim, and `release_issue` gives it back.
- **File and shape the work:** `save_issue`, `save_comment`, `add_relation`, labels and attachments.
- **See where it stands:** `queue_status`, `list_issues`, `get_issue`, analytics and usage.
- **Bring a backlog across** from Linear, Jira, Asana, ClickUp or Shortcut.

The full list, with what each tool does, is at https://docs.retasc.com/mcp-tools.

## Links

- Docs: https://docs.retasc.com
- Privacy: https://retasc.com/privacy
- Terms: https://retasc.com/terms
- Support: support@retasc.com

## License

MIT, copyright Reply200 Inc. See [LICENSE](LICENSE).

## Trademarks

Retasc and the Retasc logo, including `assets/icon.png`, are trademarks of Reply200 Inc. The MIT
License covers the code and text in this repository. It does not license the Retasc name or logo.
You may use them only to refer to Retasc and this plugin, never to name, brand or endorse another
product or service.
