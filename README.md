# Capstone Part II – Incident Response & Executive Reporting

## Purpose

This project documents the investigation and response to a simulated cybersecurity incident as part of the Code You Cybersecurity Capstone.

The investigation follows the NIST incident response lifecycle and focuses on detecting, analyzing, containing, eradicating, and recovering from suspicious activity affecting a Windows workstation.

## Scenario

A Security Operations Center (SOC) received alerts involving suspicious activity from a Finance department workstation.

The investigation identified suspicious PowerShell execution followed approximately two minutes later by repeated outbound HTTP POST requests to an external IP address.

The available evidence was correlated to assess the incident and develop appropriate response recommendations.

## Affected System

- Hostname: `DESKTOP-984`
- User: `jdoe`
- Full Name: John Doe
- Department: Finance
- Operating System: Windows 11
- Host IP: `47.82.196.43`
- Suspicious external IP: `115.83.105.236`

## Key Security Events

### Suspicious PowerShell Execution

At `2026-01-27T23:03:10Z`, security monitoring detected `powershell.exe` execution by user `jdoe` on `DESKTOP-984`.

### Suspicious Outbound Traffic

At `2026-01-27T23:05:00Z`, a high-severity alert identified repeated outbound HTTP POST requests from the affected system to external IP address `115.83.105.236`.

The close timing between these events increased the likelihood that the endpoint and network activity were related.

## Incident Response Lifecycle

The investigation follows these incident response stages:

1. Detection
2. Containment
3. Eradication
4. Recovery
5. Lessons Learned

## Deliverables

### `incident_response_report.md`

Full technical incident response report containing:

- Executive summary
- Detection and analysis
- Event correlation
- Timeline of activity
- Indicators of Compromise
- Impact assessment
- Containment actions
- Eradication actions
- Recovery procedures
- Lessons learned
- Recommendations

### `executive_briefing.md`

Leadership-focused summary containing:

- Incident overview
- Business impact
- Key findings
- Response actions
- Recovery considerations
- Leadership recommendations

## Timeline

| Time (UTC) | Activity |
|---|---|
| 2026-01-27 23:03:10 | Suspicious PowerShell execution detected |
| 2026-01-27 23:05:00 | Repeated outbound HTTP POST requests detected |

## Indicators of Compromise

- Host: `DESKTOP-984`
- User: `jdoe`
- Source IP: `47.82.196.43`
- External destination IP: `115.83.105.236`
- Process: `powershell.exe`
- Network behavior: Repeated outbound HTTP POST requests

## Assessment

The available evidence supports treating `DESKTOP-984` as potentially compromised.

The investigation does not establish that data theft occurred or identify the complete method of initial compromise. Additional endpoint, authentication, DNS, and network evidence would be required to make those determinations.

## Recommended Actions

- Isolate the affected workstation
- Block communication with the suspicious external IP
- Preserve forensic evidence
- Investigate PowerShell activity
- Review authentication activity
- Search for the identified indicators across the environment
- Reset credentials if account compromise is suspected
- Remove confirmed malicious artifacts
- Validate system integrity before recovery
- Increase monitoring after restoration

## Conclusion

This project demonstrates the SOC incident response process by correlating security alerts, identifying potentially malicious activity, assessing organizational risk, and translating technical findings into actionable recommendations for both technical personnel and executive leadership.
## AI Assistance Disclosure

AI was used as a support tool during this project to help with organization, formatting, troubleshooting, documentation structure, and explanation of cybersecurity concepts.

All project work was reviewed, tested, and approved by me. I remained responsible for understanding the code, validating the results, interpreting the findings, and explaining the final project.