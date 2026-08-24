# Cybersecurity Research Lab

> A structured, evidence-driven portfolio of cybersecurity research, threat intelligence, detection engineering, vulnerability analysis, malware analysis, and SOC investigation methodology.

![Focus](https://img.shields.io/badge/Focus-Cybersecurity-informational)
![Research](https://img.shields.io/badge/Research-Threat%20%26%20Defense-informational)
![Status](https://img.shields.io/badge/Status-Active-success)

## About

This repository is a living cybersecurity research portfolio designed around practical blue-team, SOC, threat-intelligence, vulnerability-research, and malware-analysis workflows.

The goal is not to collect disconnected notes. Each research area is organized around a repeatable process:

```text
Threat / Vulnerability
        ↓
Evidence Collection
        ↓
Technical Analysis
        ↓
Behavior & Attack Chain
        ↓
MITRE ATT&CK Mapping
        ↓
Detection Opportunities
        ↓
Investigation / Response
        ↓
Mitigation & Lessons Learned
```

## Research Areas

| Area | Focus | Primary Security Skill |
|---|---|---|
| [`ransomware-analysis/`](./ransomware-analysis/) | Ransomware families, campaigns, IoCs, ATT&CK, defenses | Threat Intelligence / IR |
| [`windows-event-log-analysis/`](./windows-event-log-analysis/) | Windows Security, Sysmon, authentication and endpoint telemetry | SOC Analysis |
| [`active-directory-attack-detection/`](./active-directory-attack-detection/) | AD attack paths and detection | Blue Team / Detection |
| [`phishing-investigation/`](./phishing-investigation/) | Email, URL, domain, attachment and identity investigation | SOC / Incident Response |
| [`vulnerability-research/`](./vulnerability-research/) | CVE analysis, root cause, exploitability, detection and mitigation | VAPT / Vulnerability Research |
| [`splunk-detection-engineering/`](./splunk-detection-engineering/) | SPL detections, tuning, ATT&CK mapping and triage | SIEM / Detection Engineering |
| [`malware-analysis/`](./malware-analysis/) | Static, dynamic, network analysis and IoC extraction | Malware Analysis / DFIR |

## Research Standards

Every substantial investigation should aim to include:

- Clear research objective
- Reliable primary or high-quality secondary references
- Evidence and reproducible observations where possible
- Attack-chain or root-cause analysis
- IoCs and behavioral indicators where appropriate
- MITRE ATT&CK mapping where applicable
- Detection opportunities
- False-positive considerations
- Mitigation and response guidance
- Confidence level and limitations
- Clear separation between fact and analyst assessment

## Detection Engineering

The repository prioritizes practical detection content rather than theory alone.

Planned detection formats include:

- **Splunk SPL**
- **Sigma**
- **Wazuh rules**
- **KQL**
- **YARA**
- Endpoint and network behavioral analytics

## SOC Investigation Model

```text
Alert
 ↓
Validate
 ↓
Identify User / Host / Process
 ↓
Build Timeline
 ↓
Correlate Telemetry
 ↓
Map ATT&CK
 ↓
Determine Scope
 ↓
Contain
 ↓
Eradicate / Recover
 ↓
Document & Improve Detection
```

## Quality Over Quantity

A small number of well-researched, evidence-backed investigations is more valuable than a large collection of copied commands or unverified threat claims.

Research should distinguish clearly between:

- **Confirmed fact**
- **Observed evidence**
- **Vendor / government reporting**
- **Analyst assessment**
- **Unverified or disputed claims**

## Repository Roadmap

- [x] Establish research structure
- [x] Ransomware evolution baseline
- [x] Research-area READMEs
- [ ] Add Windows event investigations
- [ ] Add production-quality Splunk detections
- [ ] Add AD attack-detection case studies
- [ ] Add phishing investigation cases
- [ ] Add CVE research reports
- [ ] Add malware-analysis reports
- [ ] Add reusable Sigma/YARA detections
- [ ] Add sanitized datasets and lab evidence

## Responsible Research

This repository is intended for **authorized cybersecurity research, education, threat intelligence, detection engineering, incident response, and controlled security testing**.

Only test offensive techniques against systems and environments where you have explicit authorization. Do not publish credentials, access tokens, private data, or operational secrets.

Malware and exploit research should be performed in isolated lab environments with appropriate containment.

## References

Depending on the research topic, sources may include:

- CISA
- MITRE ATT&CK
- NIST
- FBI / U.S. Department of Justice
- Europol
- Mandiant / Google Threat Intelligence
- CrowdStrike
- Microsoft Security
- Cisco Talos
- Recorded Future
- Trend Micro
- Group-IB
- BleepingComputer
- Vendor security advisories and technical research

## Research Status

**Active and continuously evolving.** New case studies, detections, vulnerability research, threat intelligence, and malware-analysis work will be added as they are validated.

---

**Author:** 1amBa7Man  
**Repository:** [`1amBa7Man/Research`](https://github.com/1amBa7Man/Research)
