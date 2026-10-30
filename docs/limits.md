[← Scarwise](../README.md)

# Limits

What Scarwise does not do yet.

What it supports is in [Works with](../README.md#works-with). What it needs is in [Requirements](../README.md#requirements).

## Mistakes it cannot see

- **A call that "succeeds" with a wrong result.** Scarwise learns from calls that fail. When a tool returns a result that looks fine but is wrong, there is nothing to learn from.
- **A mistake made only once.** The first time is always allowed: Scarwise needs to see the mistake, and then what worked, before it can stop it.
- **A tool that has never worked is still tried now and then** (after it failed in two conversations in a row, at most once a day), so a tool repaired in the meantime is found again; that try can fail once more.

## Agents

- Claude Code, Codex CLI, Gemini CLI, Cursor, Copilot CLI and Kiro CLI are covered by automated tests; their real use is being checked in the beta.
- An agent that changes its hook format in a new version may need a new Scarwise version. `scarwise init` tests every connection and tells you when one does not work.
- Web chats (Claude.ai, ChatGPT) are covered only through your own MCP server and `scarwise proxy`; their built-in tools (web search, code execution) are not.

## Shared library

- A lesson from the library applies only to a public MCP server that Scarwise recognizes in your agents' settings. A server started by your own script is not recognized.
- Library lessons only stop and explain.

## Platforms

- Node.js 22 or newer is required, also for the Python SDK (it calls the `scarwise` command).
