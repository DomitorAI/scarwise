[← Scarwise](../README.md)

# Privacy

Scarwise works on your computer. It watches the tool calls of your AI agents to learn from their mistakes, and it keeps what it learns in `~/.scarwise` on your computer.

## What stays on your computer

- The recent tool calls Scarwise has seen, the lessons it learned, its statistics and settings.
- None of this is ever sent.

## What may leave your computer

> **BOTH ARE ON BY DEFAULT**, from the install on, with no question asked. **To turn them off:** `scarwise share off` and `scarwise telemetry off` (each takes effect at once; `scarwise share` and `scarwise telemetry` show the current setting).

Only through one small relay that files reports into a private repository read by the Scarwise team. Never your tool calls, files, prompts or answers.

| What | When | Turn it off |
|---|---|---|
| The **name** of an agent Scarwise does not support yet (and its version), the operating system and the Scarwise version | **ON BY DEFAULT**; each name once | `scarwise telemetry off` |
| **Lessons for the shared library** | **ON BY DEFAULT**; the first one when it appears, then at most once a week (or when you run `scarwise share now`), each lesson once | `scarwise share off` |
| A **diagnostic file** | only when you run `scarwise report` and send the file yourself | – |

What waits to be sent is in `~/.scarwise/outbox.jsonl`; you can look at it at any time.

### Lessons for the shared library

Only general mistake patterns that Scarwise has already proven on your computer, or a tool of a public MCP server that has never worked there (named by its public package, not by the name you gave the server). Before leaving your computer they are cleaned:

- your home folder becomes `~`, your user name becomes `<user>`;
- API keys, tokens, passwords and `Bearer` headers are masked;
- whole commands are not sent, only the short examples needed to explain a lesson;
- lessons about your private MCP servers (whose package is not public) are not sent;
- a hosted MCP server (reached by URL) is named only by a one-way fingerprint of its host name – never the address, its path or its parameters; servers on your own computer or private network are never named at all, and a fingerprint that does not belong to a public server from the official MCP registry never enters the shared library;
- lessons you received from the library or from others are never sent back.

We read the reports and choose by hand what enters the library. Anything that still looks private is refused automatically.

### The relay

It accepts only small reports of known shapes and shortens every text. It keeps no addresses: a daily, salted fingerprint is used to limit the number of reports, and it expires after two days.

## Uninstall

`npm uninstall -g scarwise` removes everything: the next time each agent starts, Scarwise takes out its hooks, its OpenCode plugin and the wrapping of your MCP servers, deletes its backups and `~/.scarwise` (lessons, statistics, settings and anything still waiting to be sent).

## Updates

Scarwise checks at most once a day whether a new version exists (one request to the npm registry) and tells you at the start of each agent session. It never updates itself: `scarwise update` does it when you decide.
