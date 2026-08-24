# Windows Event Log Analysis

A practical SOC-focused research collection for investigating Windows security telemetry, Sysmon events, suspicious process activity, authentication anomalies, persistence, and endpoint attacks.

## Objectives

- Understand high-value Windows Security and Sysmon events
- Build repeatable SOC investigation workflows
- Correlate authentication, process, network, and persistence telemetry
- Develop detections for common attacker behaviors
- Map detections to MITRE ATT&CK
- Document false positives and analyst triage steps

## Core Event Coverage

| Area | Examples |
|---|---|
| Authentication | 4624, 4625, 4634, 4648 |
| Privilege | 4672 |
| Process Creation | 4688, Sysmon 1 |
| Account Changes | 4720, 4726, 4732, 4738 |
| Scheduled Tasks | 4698, 4702 |
| Services | 7045 |
| PowerShell | 4103, 4104 |
| Sysmon Network | 3 |
| Sysmon Process Access | 10 |

## Investigation Workflow

```text
Alert
 ↓
Validate Event
 ↓
Identify User / Host / Process
 ↓
Build Timeline
 ↓
Correlate Related Events
 ↓
Map ATT&CK Behavior
 ↓
Determine Scope
 ↓
Contain / Escalate
 ↓
Document Findings
```

## Detection Engineering

Planned detection formats:

- Splunk SPL
- Sigma
- Wazuh
- KQL
- Sysmon-based behavioral detections

Each detection should document the data source, query/rule, ATT&CK mapping, expected behavior, false positives, triage procedure, and response recommendation.

## High-Value SOC Scenarios

- Password spraying and brute force
- Suspicious PowerShell
- Malicious process creation
- New local accounts
- Privilege escalation
- Scheduled-task persistence
- Service creation
- RDP abuse
- Credential dumping indicators
- Lateral movement
- Defense evasion

## Quality Standard

Every investigation should preserve the original event context, explain why the behavior is suspicious, correlate supporting telemetry, distinguish evidence from analyst assessment, and provide an actionable response path.

## Safety

Use sanitized logs or authorized lab telemetry. Never collect or publish real credentials, secrets, tokens, or sensitive personal data.
