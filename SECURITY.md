# Security policy

## Reporting a vulnerability

Please **do not open a public issue** for a security problem.

Report it privately: [Security → Report a vulnerability](https://github.com/DomitorAI/scarwise/security/advisories/new).
Only the maintainers can see the report.

Include what you can:
- the part: the `scarwise` command, an agent connection (which agent), the MCP proxy, the API proxy, or an SDK;
- the version (`scarwise version`);
- the steps to reproduce;
- what an attacker could do.

Never include real API keys or personal data. A `scarwise report` file helps; look at it before sending.

You will get an answer in the report.
Once a fix is released, the advisory is published, with credit to you if you wish.

## Supported versions

Only the latest release is supported.
Fixes come as a new version. Scarwise tells you when one is out; `scarwise update` installs it.
