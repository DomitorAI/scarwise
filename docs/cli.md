[← Scarwise](../README.md)

# The `scarwise` command

**Nothing to run to get started:** `npm install -g scarwise` connects your agents by itself. Everything else is for when you want to look inside, change something, or connect what the install cannot find by itself.

> **Lesson sharing and agent-name reporting are ON BY DEFAULT.** To turn them off: `scarwise share off` and `scarwise telemetry off`.

`scarwise help <command>` shows a command's options and examples. `scarwise` with no command shows the list.

## Getting started

| Command | When to use it |
|---|---|
| `scarwise init [--dry-run]` | After you install a new agent (the install already did it for the agents you had). It finds your agents, connects Scarwise to each of them (only its own entries, with a backup of every file it changes), tests every connection and says in one line which are connected. `--dry-run` shows what it would do and changes nothing. |
| `scarwise install <agent> [--uninstall]` | To connect or disconnect one agent: `claude`, `qwen`, `opencode`, `codex`, `gemini`, `cursor`, `copilot`, `kiro`. |
| `scarwise uninstall` | To disconnect Scarwise from every agent but keep it installed. Your lessons stay in `~/.scarwise`. To remove everything: `npm uninstall -g scarwise` (the next start of each agent removes every trace). |
| `scarwise update [--check]` | When Scarwise tells you a new version exists (at the start of each agent session). It installs it and reconnects your agents. Scarwise never updates by itself. `--check` only tells you whether one exists. |
| `scarwise version` | Shows the installed version. |

## Everyday

| Command | What it does |
|---|---|
| `scarwise stats` | Mistakes prevented, time and tokens saved, the most useful lessons. |
| `scarwise lessons` | What Scarwise has learned on this computer, with the explanation of each lesson. |
| `scarwise forget <id>` | Removes a lesson you know is wrong. |
| `scarwise config level quiet\|normal\|verbose` | How much Scarwise tells you. `quiet`: no lines for you (the agent still gets the explanation). `normal` (default): one line per stopped mistake and a summary at the end of a session. `verbose`: also when a lesson is learned. |
| `scarwise share [on\|off\|now]` | Shows or changes whether you contribute to the shared library (**ON BY DEFAULT**; `off` stops it); `now` sends what is ready without waiting for the weekly batch. See [Privacy](privacy.md). |
| `scarwise telemetry [on\|off]` | Shows or changes the reporting of agent names Scarwise does not support yet. See [Privacy](privacy.md). |
| `scarwise report [file] [--no-commands]` | Makes one diagnostic file to attach to a bug report. Home paths, your user name and secrets are masked; `--no-commands` leaves out the text of commands and outputs entirely. Look at the file before sending it. |

## Moving lessons

| Command | What it does |
|---|---|
| `scarwise export [file] [--tool <name>]` | Saves your lessons to a `.scar.json` file: for another computer, or for a colleague. Home paths, your user name and secrets are masked. |
| `scarwise import <file> [--dry-run]` | Loads lessons from such a file. They only stop and explain, and are treated as untrusted. |

## Agents without hooks, web chats and your own applications

| Command | What it does |
|---|---|
| `scarwise proxy --listen <port> --upstream <url> [--name <server>]` | For **Claude.ai and ChatGPT**: Scarwise in front of an MCP server they reach through a public address. Point the tunnel to `--listen`; `--upstream` is your MCP server. Keep the window open; it reloads itself after an update without interrupting requests. Example: `scarwise proxy --listen 8080 --upstream http://127.0.0.1:9080 --name files` |
| `scarwise mcp --name <server> -- <command> [args]` | Runs a local (stdio) MCP server through Scarwise, for an agent whose hooks do not see MCP tools. `init` sets this up for OpenCode by itself. Example: `scarwise mcp --name files -- npx -y @modelcontextprotocol/server-filesystem .` |
| `scarwise run [--shell cmd\|powershell\|bash] -- <agent> [args]` | Starts an agent that has no hooks, with its shell commands going through Scarwise. Example: `scarwise run -- aider` |
| `scarwise api --listen <port> --upstream <url> --format anthropic\|openai` | For an application built directly on a model API: Scarwise in front of the API. Example: `scarwise api --listen 8099 --upstream https://api.anthropic.com --format anthropic` |

## Measuring

| Command | What it does |
|---|---|
| `scarwise ab start <run> [--observe] [--fresh]` · `stop` · `report` · `reset` | Compares the same task without and with Scarwise. `--observe`: Scarwise learns but does not intervene (the "without" runs). `report` shows failed calls, repeated mistakes, time and tokens per run, and the comparison. |
| `scarwise snapshot` / `restore` | Puts your real lessons aside to measure from an empty start, and brings them back afterwards. |
