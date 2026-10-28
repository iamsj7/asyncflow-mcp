# AsyncFlow connector

Use your [AsyncFlow](https://flow.async.om) tickets from an AI chat. You can
search, open, create, update, assign, move and comment on tickets in your own
company, with the access you choose when you connect.

The connector address is:

```text
https://flow.async.om/api/mcp
```

When you connect, a browser opens. Sign in to AsyncFlow, pick the company and
tick the access to allow. Nothing is installed on your computer, and your
AsyncFlow password never reaches the chat. You can disconnect a chat at any
time in AsyncFlow under **Settings → Connected apps**.

## Claude Code

Install the plugin. It sets up the connector and adds a skill that tells
Claude how to work with tickets safely.

```text
/plugin marketplace add iamsj7/asyncflow-mcp
/plugin install asyncflow@asyncflow
```

Then run `/mcp`, choose **asyncflow** and sign in.

To add only the connector, without the skill:

```bash
claude mcp add --transport http asyncflow https://flow.async.om/api/mcp
```

## Claude (web and desktop)

**Settings → Connectors → Add custom connector.** Name it AsyncFlow and paste
the address above.

## ChatGPT

Add a custom connector in ChatGPT's settings and paste the address above. This
needs a plan that allows custom connectors.

## Cursor

Add this to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "asyncflow": { "url": "https://flow.async.om/api/mcp" } } }
```

## VS Code

```bash
code --add-mcp '{"name":"asyncflow","type":"http","url":"https://flow.async.om/api/mcp"}'
```

## Other chats

Any client that supports remote MCP servers over streamable HTTP with OAuth
can connect. If the chat says its redirect address isn't allowed, send that
address to [Async Solution](https://asyncsolution.com) and it will be added.

## What the chat can do

| Access | What the chat can do |
|---|---|
| See the company and its workspaces | `whoami`, `list_projects` |
| Read tickets you can already read | `list_ticket_options`, `search_tickets` (board filters: created or resolved dates, due, assigned to me, SLA and more), `get_tickets`, `get_ticket`, `get_ticket_history`, `workspace_summary`, `get_attachment` (images are shown to the chat) |
| Create and manage tickets | `create_ticket`, `update_ticket` (any field, parent), `assign_ticket`, `transition_ticket`, `link_tickets`, `unlink_tickets`, `request_approval`, `decide_approval`, `log_time`, `upload_attachment`, `start_upload`, `attach_file`, `remove_attachment`, `archive_tickets`, `restore_tickets`, `list_archived_tickets` |
| Add comments | `add_comment` (with files) |

Your role in each workspace still applies, and the chat can't delete anything.
Due dates and other planning fields stay visible to the delivery team only.

## Microsoft Teams and Microsoft 365 Copilot

In Copilot Studio, create an agent, add a tool of type **Model Context
Protocol** with the address above and **OAuth 2.0, dynamic discovery**, and
publish it to the **Teams and Microsoft 365 Copilot** channel. Copilot Studio
shows a callback URL: send it to [Async Solution](https://asyncsolution.com)
so it can be allowed.

## Licence

MIT. This repository only holds the connector setup. The AsyncFlow service is
operated by Async Solution.
