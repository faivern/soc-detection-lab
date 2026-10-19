# Evidence register

This publication was prepared from the lab owner's written account. The workspace initially contained no lab artifacts. Configuration files reproduce the supplied snippets; they are not exports retrieved from the running VMs.

| Item | Available basis | What it establishes |
|---|---|---|
| SSH failure | One log excerpt supplied in the lab notes | Reported failed authentication with source, account, and port; no timestamp supplied |
| Rules `5760`, `5763`, `2502`, `5557`, `5503` | Lab owner's observations | Reported dashboard matches; original events unavailable |
| Custom rule `100101` | Complete supplied XML | Intended detection logic, not proof of a live alert |
| Validation commands | Commands and reported successful practical testing | Workflow used; no output to separate logtest results from live delivery |
| FIM | Directory configuration and before/after test values | Monitoring intent and reported modification; no exported event or diff |
| Screenshots | None available | No screenshots embedded or fabricated |

## Evidence to retain for a follow-up

Capture the installed versions and a narrow time window with timezone. Preserve sanitized alert JSON alongside screenshots when possible. A manager-generated custom alert should show `rule.id`, timestamp, Linux agent identity, source IP, and relevant raw event. A logtest transcript should be labeled as such: it tests rule evaluation, not end-to-end collection and dashboard delivery.

Suggested screenshot subjects and filenames are listed in the [screenshots guide](../assets/screenshots/README.md). These are outstanding assets, not existing images.

## Follow-up validation matrix

These are proposed tests, **not recorded results**. Use only the isolated lab and retain the input sequence and timestamps.

| Test | Expected property to investigate | Current evidence |
|---|---|---|
| Same-source burst matching `5760` | Custom correlation can produce `100101` | Successful testing reported; original output missing |
| One isolated failure | No custom burst alert with clean correlation state | Not documented |
| Failures separated beyond 20 seconds | No aggregation across the configured window | Not documented |
| Different source IPs, each below threshold | No aggregation across source IPs | Not documented |
| Successful authentication only | No match through the failure-based parent | Not documented |
| Test-file edit after FIM baseline | File-change event and, where available, text diff | No event export supplied |

For live tests, inspect both the manager alert and dashboard result. Record actual trigger behavior rather than equating keystrokes, SSH connections, log lines, and matching events. Do not infer compromise or user attribution from these tests.
