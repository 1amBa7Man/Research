# Ransomware Analysis

A defensive threat-intelligence research collection focused on the evolution, behavior, infrastructure, impact, and detection of ransomware operations.

## Objectives

- Track major ransomware families and campaigns
- Document intrusion chains and operator behavior
- Extract and organize Indicators of Compromise (IoCs)
- Map behaviors to MITRE ATT&CK
- Develop SIEM/EDR detection opportunities
- Document defensive controls and incident-response lessons

## Analysis Framework

```text
Threat / Campaign
      ↓
Initial Access
      ↓
Execution & Persistence
      ↓
Discovery & Credential Access
      ↓
Lateral Movement
      ↓
Collection & Exfiltration
      ↓
Encryption / Destruction
      ↓
Extortion
      ↓
Detection & Response
```

## Planned Research

- Ransomware family profiles
- RaaS ecosystem analysis
- Double/triple extortion
- Initial-access-broker relationships
- Windows and Active Directory attack paths
- Backup destruction and recovery inhibition
- Ransomware detection engineering
- IoC and behavioral intelligence
- Incident case studies

## Detection Coverage

Planned formats:

- Sigma
- Splunk SPL
- Wazuh rules
- MITRE ATT&CK mappings
- Network indicators
- Endpoint behavioral indicators

## Current Research

See the main repository report: [`../ransomware-evolution.md`](../ransomware-evolution.md).

## Methodology

Each investigation should separate confirmed facts, vendor/law-enforcement reporting, observed IoCs, analyst assessment, and unresolved attribution claims.

## Safety

All analysis is intended for authorized defensive research, malware analysis, threat intelligence, and controlled lab environments. Do not deploy ransomware or other malicious tooling against systems without explicit authorization.

## Quality Standard

A completed case study should include evidence, reliable references, attack-chain analysis, IoCs where appropriate, ATT&CK mapping, detection opportunities, mitigations, and a clear distinction between fact and assessment.
