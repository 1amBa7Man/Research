# Phishing Investigation

A practical SOC investigation framework for analyzing suspicious emails, URLs, domains, attachments, authentication signals, and related Indicators of Compromise.

## Objectives

- Investigate phishing alerts systematically
- Analyze email authentication and headers
- Assess URLs, domains, attachments, and redirects
- Extract actionable IoCs
- Correlate phishing activity with endpoint and identity telemetry
- Produce concise incident reports

## Investigation Workflow

```text
Suspicious Email
      ↓
Header Analysis
      ↓
SPF / DKIM / DMARC
      ↓
Sender & Domain Analysis
      ↓
URL / Redirect Analysis
      ↓
Attachment Analysis
      ↓
Reputation / Sandbox Analysis
      ↓
IOC Extraction
      ↓
SIEM / EDR Correlation
      ↓
Scope Assessment
      ↓
Containment & User Remediation
```

## Analysis Areas

- Email headers
- Sender identity and spoofing indicators
- SPF, DKIM, and DMARC
- Lookalike and newly registered domains
- URL reputation and redirect chains
- Malicious attachments
- Macro/script indicators
- Credential-harvesting pages
- Browser and endpoint telemetry
- User interaction and authentication anomalies

## Investigation Output

Each case should produce:

- Executive summary
- Timeline
- Attack vector
- Affected users/assets
- IoCs
- Evidence and confidence
- MITRE ATT&CK mapping where applicable
- Containment actions
- Eradication/recovery recommendations
- Lessons learned

## IoC Categories

```text
Email addresses
Domains
URLs
IP addresses
File hashes
Attachment names
Sender infrastructure
Authentication artifacts
```

## Quality Standard

Do not label an email malicious based on a single weak signal. Combine authentication results, infrastructure reputation, message content, URL behavior, attachment evidence, and endpoint/identity telemetry.

## Safety & Privacy

Use sanitized samples whenever possible. Never publish real credentials, tokens, private email content, or personally identifiable information.
