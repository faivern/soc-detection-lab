# Evidence register

The case combines the lab owner's notes with eight original screenshots. Seven are embedded in the case; the editor capture is linked here because the rule is easier to read and reuse as XML. Images were reviewed for visible secrets and unrelated content and retained without pixel edits. Raw alert JSON and validation transcripts are not included.

| Evidence | What is visible | Limit |
|---|---|---|
| [SSH client](../assets/screenshots/01-ssh-attack.png) | Connection to `soclab@192.168.142.134` and repeated rejected password prompts | Does not establish the full correlation sequence |
| [Linux authentication logs](../assets/screenshots/02-ssh-authentication-logs.png) | Failed passwords from `192.168.142.131`, target account, hostname, and local times | No year or timezone in the journal crop |
| [Threat Hunting](../assets/screenshots/03-wazuh-threat-hunting.png) | Rules `5760`, `5557`, `5503`, `2502`, and connection-reset rule `5762`; agent `ubuntu-user` | Built-in brute-force rule `5763` remains a lab-note observation |
| [Rule editor](../assets/screenshots/04-custom-detection-rule.png) | `local_rules.xml` with rule `100101`, frequency 5, timeframe 20, and parent `5760` | Editor shows a modified buffer; this image alone does not prove saving or deployment |
| [Custom alert](../assets/screenshots/05-custom-rule-alert.png) | Dashboard document with `100101`, level 10, source IP, user, `journald`, previous failures, and ATT&CK mapping | Proves live alert delivery; does not establish total attempts or logtest output |
| [FIM event row](../assets/screenshots/06-file-integrity-monitoring-row.png) | Rule `550`, level 7, `modified`, test path, and Linux agent | File change is not proof of compromise |
| [FIM event details](../assets/screenshots/06-file-integrity-monitoring-details.png) | Actual text diff, realtime mode, changed hashes, size, and modification time | Ownership fields do not identify the editing user |
| [FIM inventory](../assets/screenshots/07-fim-inventory.png) | File attributes, hashes, size 18 bytes, and `soclab` ownership | Inventory is not an audit trail of user actions |

## Time interpretation

The custom alert's dashboard timestamp is October 19, 2026, 19:38:54.185, while its raw SSH log shows 17:38:52. The FIM row displays October 19, 2026, 22:14:24.242; its details show a file modification time of October 20, 00:14:24, while inventory displays October 19, 22:14:24. These are transcribed display values, not normalized UTC timestamps.

Clock and timezone settings were not supplied. Resolve these differences before comparing elapsed times or asserting a precise cross-event sequence. The screenshots establish separate SSH and FIM detections, not an automatic correlation or causal relationship.

## Validation status

| Test | Evidence and outcome |
|---|---|
| Positive same-source SSH burst | Live custom alert `100101` captured in the dashboard |
| Configuration validation | `wazuh-analysisd -t` documented in notes; output unavailable |
| Rule evaluation in logtest | Successful practical testing reported; logtest transcript unavailable |
| Negative test | Text-only procedure in the case; exact execution and observed result not supplied |
| Slow guessing and distributed sources | Proposed follow-up tests, not recorded results |
| Test-file modification | Rule `550` event and actual `syscheck.diff` captured |

For future runs, retain the installed versions, timestamped inputs, timezone settings, and narrow sanitized alert exports. For a negative result, verify that the base events arrived and that the search covered the correct agent, source, and time window. An empty alert search without that control does not establish correct detection behavior.
