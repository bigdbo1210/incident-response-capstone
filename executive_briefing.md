# Capstone Part II – Executive Incident Briefing

## Incident Overview

A high-severity cybersecurity incident was identified involving `DESKTOP-984`, a Windows 11 workstation assigned to Finance department user `jdoe` (John Doe).

At `23:03:10 UTC` on January 27, 2026, security monitoring detected suspicious PowerShell execution on the workstation.

Approximately two minutes later, at `23:05:00 UTC`, the same system generated repeated outbound HTTP POST requests to external IP address `115.83.105.236`. The network activity triggered a high-severity IDS alert.

The close timing between the PowerShell execution and suspicious outbound communication indicates that the activities may be related. The workstation should therefore be treated as potentially compromised until further investigation is completed.

## Business Impact

Because the affected workstation belongs to the Finance department, unauthorized access could potentially expose sensitive organizational or financial information.

At this stage, the available evidence does not confirm that sensitive information was stolen. However, the suspicious outbound communication requires further investigation to determine whether unauthorized data transmission occurred.

## Key Findings

- Affected host: `DESKTOP-984`
- Affected user: `jdoe` (John Doe)
- Department: Finance
- Operating system: Windows 11
- Suspicious PowerShell execution detected
- Repeated outbound HTTP POST requests detected
- External destination: `115.83.105.236`
- Network alert severity: High
- Potential malware or command-and-control activity requires investigation

## Response Actions

The recommended response is to immediately isolate the affected workstation from the network while preserving evidence.

Security personnel should block communication with the suspicious external IP address, investigate PowerShell activity, review authentication and endpoint logs, and search the environment for other systems displaying the same indicators.

If account compromise is suspected, credentials associated with the affected user should be reset.

Any confirmed malware, unauthorized scripts, persistence mechanisms, or malicious configurations should be removed before the workstation is returned to normal operation.

## Recovery

The affected system should only be restored to the corporate network after security personnel verify that it is in a trusted state.

Following recovery, the workstation and user account should receive increased monitoring to ensure that suspicious activity does not return.

## Leadership Recommendations

Leadership should support:

1. Enhanced PowerShell monitoring and logging.
2. Improved endpoint detection and response capabilities.
3. Centralized correlation of endpoint, authentication, DNS, and network security logs.
4. Rapid isolation procedures for potentially compromised systems.
5. Continued cybersecurity awareness training for employees.
6. Periodic incident response exercises and review of response procedures.

## Conclusion

The incident presents a credible security concern because suspicious PowerShell execution was followed within approximately two minutes by high-severity outbound network activity.

Although the available evidence does not prove data theft or establish the complete method of compromise, the activity warrants containment and further forensic investigation.

Rapid containment, evidence preservation, investigation, eradication, and controlled recovery will reduce the potential impact to the organization.