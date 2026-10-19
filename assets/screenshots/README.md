# Screenshot evidence

No screenshots were available for the initial publication. This directory intentionally contains no illustrative dashboard images or broken image placeholders.

When original captures become available, use these suggested names:

| Filename | Evidence to show |
|---|---|
| `soc-001-01-ssh-attempts.png` | PowerShell connection and failed authentication |
| `soc-001-02-linux-auth-events.png` | Threat Hunting records from the Linux agent |
| `soc-001-03-builtin-bruteforce.png` | Built-in rule `5763` event details |
| `soc-001-04-custom-logtest.png` | Rule `100101` evaluation, clearly labeled logtest |
| `soc-001-05-custom-manager-alert.png` | Actual manager-generated `100101` alert, if retained |
| `soc-001-06-fim-event.png` | Monitored path, event time, and changed metadata or hashes |
| `soc-001-07-fim-diff.png` | Actual `syscheck.diff`, only if present |

Crop unrelated interface areas while retaining enough context to identify the event, source, and time. Redact credentials, tokens, unrelated infrastructure, and sensitive file contents. Keep timestamps and timezones readable for timeline analysis. Embed reviewed images in the case using relative paths and a short explanation of what each demonstrates.

Architecture is already represented by reproducible Mermaid diagrams. XML belongs in code blocks and rule files, not screenshots.
