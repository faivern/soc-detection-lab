# SOC Detection Lab

**From authentication failures to detection logic and file-change investigation.**

A personal security monitoring lab built with Wazuh in VMware Workstation. The first case follows a controlled SSH password-guessing simulation, investigation of Linux authentication events, a custom correlation rule, and a separate file integrity monitoring exercise.

**Stack:** Wazuh SIEM · Ubuntu Linux · Windows 11 · OpenSSH · VMware Workstation · MITRE ATT&CK

## Lab at a glance

```mermaid
flowchart LR
    subgraph NAT["VMware NAT · 192.168.142.0/24"]
        W["Windows 11 client<br/>192.168.142.131"]
        L["Ubuntu endpoint<br/>192.168.142.134<br/>sshd + Wazuh Agent + FIM"]
        S["Ubuntu Wazuh server<br/>Manager · Indexer · Dashboard"]
        W -->|"SSH attempts · TCP 22"| L
        L -->|"Authentication + file-change events"| S
        W -.->|"Separate Windows agent telemetry"| S
    end
    classDef endpoint fill:#e8f1ff,stroke:#3264a8,color:#14243b
    classDef server fill:#e6f5ee,stroke:#237a57,color:#123c2b
    class W,L endpoint
    class S server
```

SSH authentication evidence originates on the **Linux endpoint**. The Windows machine supplies the test traffic; its agent is not the source of these SSH detections. [Architecture details →](docs/architecture.md)

## Case studies

| Case | Investigation | Status |
|---|---|---|
| [SOC-001](cases/SOC-001-ssh-bruteforce.md) | SSH brute force, custom detection, and FIM | Completed; live custom alert and FIM diff captured |

**Key finding:** individual SSH failures matched rule `5760` in this environment, and Wazuh's existing brute-force rule `5763` was also observed. The custom rule explores correlation thresholds; it does not fill a claimed absence of built-in detection.

> **Evidence:** screenshots show Linux authentication failures, custom alert `100101`, and FIM rule `550` with the actual configuration diff. Exact triggering counts and negative-test outcomes remain undocumented. See the [illustrated case study](cases/SOC-001-ssh-bruteforce.md) and [evidence register](docs/evidence.md).

## Skills demonstrated

- Configuring a multi-VM monitoring environment and troubleshooting SSH connectivity.
- Investigating authentication events and selecting correlation rules from observed matches.
- Developing Wazuh XML rules with source-IP correlation and ATT&CK mapping.
- Configuring FIM and separating suspicious activity from proof of compromise.
- Explaining validation boundaries, false positives, and detection gaps.

## Explore the repository

[Technical case](cases/SOC-001-ssh-bruteforce.md) · [Custom rule](rules/ssh-bruteforce.xml) · [FIM configuration](configs/fim-syscheck.xml) · [Evidence register](docs/evidence.md)

## Potential extensions

These are ideas, **not completed cases**:

- **SOC-002:** Windows persistence detection.
- **SOC-003:** Automated threat response.
- **SOC-004:** Linux audit and suspicious command execution.

All activity described was a controlled simulation on personally managed lab VMs. No real-world breach or automated response is claimed.

[MIT License](LICENSE)
