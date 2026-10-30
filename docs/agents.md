[← Scarwise](../README.md)

# Agents

`npm install -g scarwise` (and later `scarwise init`, after you install a new agent) connects Scarwise to every agent it finds. This page says what it does for each one, and how to connect what it cannot find by itself.

Every change is limited to Scarwise's own entries, with a backup of the file. `scarwise uninstall` takes them out again; after `npm uninstall -g scarwise` the next start of each agent takes them out by itself.

## Agents with hooks

| Agent | What `init` adds | Where |
|---|---|---|
| Claude Code | hooks before and after each tool call, at the start of a session and at the end of a turn (session summary) | `~/.claude/settings.json` |
| Qwen Code | hooks before and after each tool call, and at the start of a session | `~/.qwen/settings.json` |
| Codex CLI | hooks before and after each tool call, at the start of a session and at the end of a turn | `~/.codex/hooks.json` |
| Gemini CLI | hooks before and after each tool call, at the start of a session and at the end of a turn | `~/.gemini/settings.json` |
| Cursor | hooks before and after each tool call | `~/.cursor/hooks.json` |
| Copilot CLI | hooks before and after each tool call | `~/.copilot/hooks/scarwise.json` |
| Kiro CLI | hooks before and after each tool call | `~/.kiro/hooks/scarwise.json` |
| OpenCode | a plugin; its local MCP servers are started through Scarwise (`scarwise mcp`) | `~/.config/opencode/` |

Start a new session of each agent after `init`. From then on, every time an agent starts you see `🛡 Protected by Scarwise` – shown to you only, never to the model (Claude Code, Codex CLI, Gemini CLI, Qwen Code; a notification in OpenCode). Cursor, Copilot CLI and Kiro CLI have no way to show it.

A lesson about an **MCP server** helps every agent that uses that server. A lesson about an agent's **own shell** stays with that agent; another agent that runs the same shell gets its fix when it makes the same mistake.

## Claude.ai and ChatGPT

Web chats reach your MCP server through a public address (for example a Cloudflare Tunnel). Put Scarwise in front of the server and point the tunnel to Scarwise:

```
your tunnel → scarwise proxy (:8080) → your MCP server (:9080)
```

```
scarwise proxy --listen 8080 --upstream http://127.0.0.1:9080 --name files
```

Keep that window open. After `scarwise update` it reloads itself without dropping the requests in progress.

## Agents without hooks

```
scarwise run -- <agent>
```

The agent's shell commands go through Scarwise. Use `--shell cmd|powershell|bash` when the agent expects a specific shell.

## Your own application

**JavaScript / TypeScript**
```js
import { guard, ScarwiseStop } from 'scarwise/sdk';

const runQuery = guard('db.query', async ({ sql }) => db.query(sql));
try {
  await runQuery({ sql: 'select 1' });
} catch (e) {
  if (e instanceof ScarwiseStop) console.log(e.message);   // the known mistake and what worked
}
```

**Python** (needs the `scarwise` command installed)
```python
from scarwise import guard, ScarwiseStop

@guard("db.query")
def run_query(sql): ...
```

**An application built directly on the Anthropic or OpenAI API:**
```
scarwise api --listen 8099 --upstream https://api.anthropic.com --format anthropic
```
Point the application's API address to `http://127.0.0.1:8099`.

## An agent Scarwise does not know yet

It is not connected. Its name is reported to us (**ON BY DEFAULT**, off: `scarwise telemetry off`) – only the name – so we know what to support next. Meanwhile `scarwise run` or `scarwise mcp` usually covers it.
