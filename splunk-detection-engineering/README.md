# Splunk Detection Engineering

A practical detection-engineering collection focused on turning security telemetry into actionable Splunk detections for SOC investigations.

## Objectives

- Build high-signal SPL detections
- Map detections to MITRE ATT&CK
- Explain data requirements and field assumptions
- Reduce false positives through context and correlation
- Document analyst triage and response actions

## Detection Lifecycle

```text
Threat Behavior
      ↓
Telemetry Requirement
      ↓
Field Normalization
      ↓
SPL Detection
      ↓
Validation
      ↓
False-Positive Tuning
      ↓
ATT&CK Mapping
      ↓
Alert Triage
      ↓
Response
```

## Detection Coverage

Planned scenarios include:

- Brute force
- Password spraying
- Port scanning
- Suspicious PowerShell
- Malicious process creation
- Credential-dumping indicators
- Persistence
- Privilege escalation
- Lateral movement
- Ransomware behavior
- Cobalt Strike-like beaconing indicators
- Suspicious LOLBins
- Data exfiltration

## Detection Template

Each rule should document:

| Field | Purpose |
|---|---|
| Detection | What behavior is detected |
| Data source | Required telemetry |
| SPL | Search logic |
| ATT&CK | Technique mapping |
| Severity | Suggested risk level |
| False positives | Expected benign matches |
| Triage | Analyst investigation |
| Response | Recommended action |

## Example Data Sources

- Windows Security
- Sysmon
- Wazuh
- Firewall logs
- Proxy logs
- DNS logs
- Authentication telemetry
- Endpoint telemetry

## Engineering Principles

Prefer behavioral and contextual detections over brittle single-string signatures. Clearly state required fields, assumptions, time windows, aggregation logic, and tuning guidance.

## Validation

Detections should be tested against representative benign and suspicious telemetry before being considered production-ready. Do not claim a detection is effective without validation evidence.

## Safety

All simulations must occur in authorized environments. Do not generate or deploy malicious activity against systems without permission.
