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
| Read tickets you can already read | `list_ticket_options`, `search_tickets`, `get_ticket` |
| Create, edit, assign and move tickets | `create_ticket`, `update_ticket`, `assign_ticket`, `transition_ticket` |
| Add comments | `add_comment` |

Your role in each workspace still applies, and the chat can't delete anything.
Files are listed by name only. To open them, use the AsyncFlow website.

## Licence

MIT. This repository only holds the connector setup. The AsyncFlow service is
operated by Async Solution.
