# Security Operations – Home Lab Monitoring Project

> A practical SOC home lab demonstrating real-time security monitoring, alert triage, investigation, escalation, and incident documentation using Wazuh, ELK/Kibana, Snort, and Sysmon.

![Wazuh](https://img.shields.io/badge/Wazuh-SIEM%20%2F%20XDR-informational)
![ELK](https://img.shields.io/badge/ELK-Kibana-informational)
![Snort](https://img.shields.io/badge/Snort-Network%20IDS-informational)
![Sysmon](https://img.shields.io/badge/Sysmon-Endpoint%20Telemetry-informational)
![Status](https://img.shields.io/badge/Status-Active-success)

## Project Overview

This independent project simulates a security operations environment where endpoint and network telemetry is collected, correlated, monitored, and investigated as alerts are generated.

The lab focuses on the analyst workflow rather than simply installing security tools:

```text
System / Network Activity
          ↓
   Sysmon / Snort
          ↓
   Wazuh / ELK
          ↓
     Alert Generated
          ↓
      Alert Triage
          ↓
   Severity Assessment
          ↓
     Investigation
          ↓
   ┌──────┴──────┐
   ↓             ↓
False Positive   True Positive
   ↓             ↓
Close          Escalate
                 ↓
          Incident Report
```

## Objectives

- Build a continuously monitored home SOC environment.
- Generate and observe security telemetry in real time.
- Review alerts as they arrive and determine severity.
- Distinguish false positives from events requiring investigation.
- Investigate suspicious endpoint and network activity.
- Document findings for audit, handoff, and incident response.
- Practice the triage-and-escalation workflow expected from a SOC analyst.

## Technology Stack

| Component | Role |
|---|---|
| **Wazuh** | Security monitoring, alerting, endpoint telemetry and correlation |
| **ELK / Kibana** | Log analysis, search, visualization and dashboards |
| **Snort** | Network intrusion detection and traffic-based alerts |
| **Sysmon** | Detailed Windows endpoint telemetry |
| **Windows/Linux endpoints** | Monitored lab systems |

## Monitoring Workflow

1. Generate normal and suspicious activity in the isolated lab.
2. Collect endpoint telemetry through Sysmon and Wazuh.
3. Monitor network activity with Snort.
4. Centralize and visualize relevant events through ELK/Kibana.
5. Validate incoming alerts.
6. Determine severity and potential impact.
7. Correlate logs and investigate suspicious behavior.
8. Classify the alert as false positive, benign, suspicious, or confirmed malicious activity.
9. Close, investigate further, or escalate based on the verdict.
10. Document the investigation and lessons learned.

## Alert Triage Model

| Priority | Analyst Action |
|---|---|
| Informational | Review and close when expected |
| Low | Validate context and monitor |
| Medium | Investigate supporting telemetry |
| High | Investigate promptly and consider escalation |
| Critical | Escalate immediately and determine scope/response |

## Evidence & Screenshots

Screenshots are intentionally separated by tool so the repository can be updated as the lab evolves.

### Architecture

Add your final lab architecture diagram here:

`![Lab Architecture](screenshots/architecture/home-lab-architecture.png)`

### Wazuh

Add Wazuh dashboard and alert screenshots here.

`![Wazuh Alerts](screenshots/wazuh/wazuh-alerts.png)`

### Kibana / ELK

Add Kibana dashboards, searches, and visualizations here.

`![Kibana Dashboard](screenshots/kibana/kibana-dashboard.png)`

### Snort

Add Snort detection output or alert screenshots here.

`![Snort Alert](screenshots/snort/snort-alert.png)`

### Sysmon

Add relevant Windows Event Viewer / Sysmon event screenshots here.

`![Sysmon Event](screenshots/sysmon/sysmon-event.png)`

## Incident Investigations

Each investigation follows a repeatable analyst format:

```text
Alert → Validate → Scope → Correlate → Investigate → Verdict → Action → Report
```

| Incident | Source | Severity | Verdict | Report |
|---|---|---|---|---|
| Incident 001 | Wazuh / Sysmon | TBD | TBD | [Report](investigations/incident-001/report.md) |
| Incident 002 | Snort | TBD | TBD | [Report](investigations/incident-002/report.md) |
| Incident 003 | Wazuh / ELK | TBD | TBD | [Report](investigations/incident-003/report.md) |

## Incident Report Template

See [`reports/incident-report-template.md`](reports/incident-report-template.md).

Each report records:

- Trigger and alert source
- Timestamp
- Affected host
- Source/destination information
- Relevant processes, users, and events
- Initial severity
- Investigation steps
- Correlated evidence
- MITRE ATT&CK mapping where applicable
- Final verdict
- Action taken
- Escalation decision
- Lessons learned

## Lab Evidence

Sanitized PCAPs, example logs, and other non-sensitive evidence can be documented under [`pcaps/`](pcaps/) and [`logs/`](logs/).

**Never commit passwords, API keys, tokens, private IP documentation, personal data, or other sensitive information.**

## Skills Demonstrated

- SOC monitoring
- Alert triage
- Incident investigation
- SIEM analysis
- Endpoint monitoring
- Network intrusion detection
- Log analysis
- Event correlation
- Severity assessment
- False-positive analysis
- Incident documentation
- Escalation decision-making
- MITRE ATT&CK-based investigation

## Disclaimer

This project is an authorized home-lab environment created for cybersecurity learning, portfolio development, and defensive security practice. All testing should be performed only against systems and networks you own or have explicit permission to test.

## Author

**Paramananda Gaigaria (1amBa7Man)**
