# Capstone Part II – Incident Response Report

## Incident Title
Suspicious PowerShell Execution and Outbound Network Communication

## Incident Classification
High-Severity Security Incident

## Executive Summary

A security incident was identified involving the Windows 11 workstation `DESKTOP-984`, assigned to Finance department user `jdoe` (John Doe).

The investigation identified suspicious PowerShell execution followed shortly afterward by repeated outbound HTTP POST requests to an external IP address.

At `2026-01-27T23:03:10Z`, an alert identified `powershell.exe` execution by user `jdoe` on `DESKTOP-984`.

Approximately two minutes later, at `2026-01-27T23:05:00Z`, a high-severity alert identified repeated outbound HTTP POST requests from the affected system to external IP address `115.83.105.236`.

The sequence of events is suspicious because PowerShell can be used by attackers to execute commands, download malicious content, or interact with compromised systems. The subsequent outbound communication may indicate malware-related activity or command-and-control communication.

Based on the available evidence, `DESKTOP-984` should be treated as potentially compromised until additional investigation confirms otherwise.

---

## Affected System

- Hostname: `DESKTOP-984`
- IP Address: `47.82.196.43`
- User: `jdoe`
- Full Name: John Doe
- Operating System: Windows 11
- Department: Finance
- Network Note: Externally routable IP assigned through corporate VPN

---

## Detection

The incident was detected through security alerts associated with suspicious endpoint and network activity.

### Alert 1 – Suspicious PowerShell Execution

- Time: `2026-01-27T23:03:10Z`
- Severity: Medium
- Source IP: `47.82.196.43`
- User: `jdoe`
- Host: `DESKTOP-984`
- Activity: `powershell.exe` execution

PowerShell is a legitimate Windows administration tool, but it is also frequently abused to execute scripts and commands. The execution becomes more significant when correlated with the suspicious network activity that occurred shortly afterward.

### Alert 2 – Suspicious Outbound Traffic

- Time: `2026-01-27T23:05:00Z`
- Severity: High
- Source IP: `47.82.196.43`
- Destination IP: `115.83.105.236`
- Protocol/Activity: Repeated outbound HTTP POST requests
- Detection Source: IDS signature

The repeated outbound HTTP POST requests to an external IP address represent the strongest network indicator in the incident.

---

## Analysis and Correlation

The two alerts are associated with the same affected system and occurred within approximately two minutes of each other.

The observed sequence was:

1. User `jdoe` was associated with PowerShell execution on `DESKTOP-984`.
2. The host subsequently generated repeated outbound HTTP POST requests.
3. The outbound traffic was directed to external IP address `115.83.105.236`.
4. The IDS classified the outbound communication as suspicious.

This correlation increases the likelihood that the PowerShell execution and outbound network communication are related.

The available evidence supports a potential compromise; however, the provided alerts alone do not prove exactly what commands were executed or what data may have been transmitted.

---

## Incident Timeline

| Time (UTC) | Event | Severity |
|---|---|---|
| 2026-01-27 23:03:10 | Suspicious PowerShell execution by `jdoe` on `DESKTOP-984` | Medium |
| 2026-01-27 23:05:00 | Repeated outbound HTTP POST requests from `47.82.196.43` to `115.83.105.236` | High |

The approximately two-minute interval between PowerShell execution and suspicious outbound traffic is an important correlation point in the investigation.

---

## Indicators of Compromise

### Host Indicators

- Hostname: `DESKTOP-984`
- Source IP: `47.82.196.43`
- User: `jdoe`
- Process: `powershell.exe`

### Network Indicators

- External destination IP: `115.83.105.236`
- Repeated outbound HTTP POST activity

These indicators should be used to search additional endpoint, firewall, proxy, DNS, authentication, and network logs for related activity.

---

## Impact Assessment

The affected workstation belongs to the Finance department, which increases the potential business impact of the incident.

Potential risks include:

- Unauthorized access to the workstation
- Malware execution
- Unauthorized external communication
- Credential compromise
- Exposure of financial or organizational information
- Additional attacker activity from the affected endpoint

The available evidence does not establish that sensitive information was successfully stolen. Therefore, data exfiltration should be investigated but should not be reported as confirmed.

---

## Containment

Recommended immediate containment actions include:

1. Isolate `DESKTOP-984` from the corporate network.
2. Block communication with `115.83.105.236`.
3. Preserve relevant logs and endpoint evidence.
4. Temporarily restrict or reset credentials associated with `jdoe` if compromise is suspected.
5. Search the environment for additional systems communicating with the same external IP.
6. Monitor for additional suspicious PowerShell activity.

Containment should preserve evidence whenever possible so that additional forensic analysis can be performed.

---

## Eradication

After containment, the security team should:

1. Perform endpoint malware scanning and forensic analysis.
2. Review PowerShell logs and command history.
3. Identify unauthorized scripts, files, scheduled tasks, or persistence mechanisms.
4. Remove confirmed malicious files or configurations.
5. Reset compromised credentials.
6. Patch applicable operating system and application vulnerabilities.
7. Confirm that no additional hosts show related indicators.

If system integrity cannot be confidently restored, the workstation should be rebuilt from a known-good image.

---

## Recovery

Recovery actions should include:

1. Restore the workstation to a trusted state.
2. Confirm endpoint security tools are operational and updated.
3. Verify that malicious processes or persistence mechanisms are no longer present.
4. Restore network access only after security validation.
5. Closely monitor the host after restoration.
6. Monitor the user's account for unusual authentication activity.
7. Confirm that communication with the suspicious external IP has stopped.

---

## Lessons Learned

This incident demonstrates the importance of correlating endpoint alerts with network activity.

A single PowerShell execution may be legitimate. However, PowerShell execution followed shortly afterward by IDS-detected outbound communication creates a stronger indication of potentially malicious behavior.

Future improvements should include:

- Enhanced PowerShell logging
- Centralized endpoint and network log correlation
- Alerting on unusual PowerShell behavior
- Monitoring repeated outbound HTTP POST activity
- Improved detection of suspicious external destinations
- Strong endpoint detection and response controls
- Regular user security awareness training
- Documented procedures for rapid workstation isolation

---

## Recommendations

1. Investigate the complete PowerShell execution history for `DESKTOP-984`.
2. Review all traffic involving `115.83.105.236`.
3. Search enterprise logs for other hosts communicating with the same destination.
4. Review authentication activity associated with `jdoe`.
5. Conduct endpoint forensic analysis before returning the system to production.
6. Reset credentials if evidence suggests account compromise.
7. Strengthen monitoring for PowerShell and suspicious outbound HTTP traffic.
8. Document and retain all evidence associated with the incident.

---

## Conclusion

The investigation identified suspicious activity involving Finance workstation `DESKTOP-984` and user `jdoe`.

The key sequence consisted of suspicious PowerShell execution at `23:03:10 UTC`, followed approximately two minutes later by repeated outbound HTTP POST requests to external IP address `115.83.105.236`.

The correlation between endpoint execution and subsequent network activity supports treating the workstation as potentially compromised.

Immediate containment, deeper endpoint investigation, credential review, eradication of any identified malicious artifacts, and controlled recovery are recommended.

The incident demonstrates how correlating multiple security data sources allows a SOC analyst to move from an individual alert toward an evidence-based assessment of potentially malicious activity.

