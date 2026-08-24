# Active Directory Attack Detection

A defensive research collection covering common Active Directory attack paths, Windows telemetry, detection engineering, and investigation workflows.

## Objectives

- Understand how common AD attacks appear in telemetry
- Identify authentication and privilege-abuse patterns
- Map attack behavior to MITRE ATT&CK
- Build detections for SOC environments
- Document investigation and containment procedures

## Attack Coverage

- Kerberoasting
- AS-REP Roasting
- Password spraying
- Pass-the-Hash
- Pass-the-Ticket
- DCSync
- Golden Ticket
- Silver Ticket
- LDAP reconnaissance
- BloodHound-style relationship discovery
- Remote service and administrative-share abuse

## Defensive Workflow

```text
Attack Technique
      ↓
Windows / AD Telemetry
      ↓
Detection Rule
      ↓
Alert Triage
      ↓
Identity + Host Correlation
      ↓
Scope Assessment
      ↓
Containment
      ↓
Credential / Access Remediation
```

## Telemetry Sources

- Windows Security logs
- Sysmon
- Directory Services logs
- PowerShell logs
- EDR telemetry
- DNS and network telemetry
- SIEM correlation data

## Detection Standard

Each technique should include:

1. Attack objective
2. Preconditions and affected components
3. Observable telemetry
4. MITRE ATT&CK mapping
5. Detection logic
6. False positives
7. Analyst triage steps
8. Containment and remediation

## Example Detection Themes

- Abnormal service-ticket requests
- Authentication anomalies
- Privileged account behavior
- Replication-rights abuse
- Unusual remote administration
- Suspicious LDAP enumeration
- New privileged group membership

## Safety

Research should be performed only in isolated labs or systems for which explicit authorization exists. Do not test attacks against third-party infrastructure.
