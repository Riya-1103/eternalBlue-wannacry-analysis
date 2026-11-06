# Final Assessment Report

## EternalBlue Exploitation and WannaCry Ransomware Analysis

**Assessment type:** Controlled cybersecurity lab assessment and malware
behaviour observation\
**Attacker environment:** Kali Linux\
**Target environment:** Windows 7 virtual machine\
**Virtualization platform:** VMware Workstation\
**Assessment status:** Lab exercise completed; 

> **Safety and scope statement:** This report documents an exercise
> performed in an isolated virtual environment. An actual WannaCry
> malware sample was used in the lab. The sample itself and any malware
> payloads are intentionally excluded from this report and repository.

------------------------------------------------------------------------

## 1. Executive Summary

This project documents a controlled cybersecurity exercise involving SMB
vulnerability investigation, EternalBlue exploitation, and subsequent
WannaCry malware execution on a Windows 7 virtual machine.

Nmap was used for host discovery, service enumeration, and vulnerability
investigation. The SMB vulnerability associated with Microsoft's
MS17-010 security bulletin was selected for validation. Metasploit's
EternalBlue module was used, and a session with the target was reported
as successfully established.

Following exploitation, the WannaCry sample was transferred and executed
through the established session in the isolated virtual environment. The
reported effects were file encryption or inaccessibility and the display
of a ransom notification.

The exercise demonstrates the potential relationship between
exploitation of a vulnerable service, unauthorized program execution,
and ransomware-related disruption. It also provides a basis for
discussing SOC detection opportunities and incident-response measures.

**Scope limitation:** The exercise demonstrates EternalBlue exploitation
followed by sample execution. It does not establish that WannaCry itself
propagated through SMB during this experiment.

## 2. Objectives

-   Identify the target host and exposed services in the lab network.
-   Investigate the target's SMB service for the vulnerability
    associated with MS17-010.
-   Validate the selected vulnerability using Metasploit in the
    authorized lab.
-   Document malware execution performed through the established
    session.
-   Record the observed effects on the target environment.
-   Identify relevant detection opportunities and defensive
    recommendations.

## 3. Scope and Lab Environment

The assessment was limited to the designated virtual machines in the
VMware lab.

  |Component                |Details|
  |---------------|- -----------------|
 |Attacker machine |         Kali Linux|
 |Target machine|            Windows 7|
  |Virtualization platform   |VMware Workstation|
  |Reconnaissance tool |      Nmap|
  |Exploitation framework |   Metasploit Framework|
  |Exploitation technique|    EternalBlue|
  |Vulnerability reference  | MS17-010; associated CVE-2017-0144|
  |Malware    |               WannaCry sample|
 | Network environment |      Isolated virtual lab|

### 3.1 IP Address Verification

The working notes reference the following addresses:

  |Machine / observation  | Address in working notes     |Publication status|              
  |-----------------------| ----------------------- |-----------------------|
  |Kali Linux             | `192.168.91.128`        |Verify against final screenshots|                                  
  |Windows 7               |`192.168.91.129`       | Verify against final screenshots|


## 4. Methodology

The exercise followed these stages:

1.  Reconnaissance and host discovery.
2.  Port and service enumeration.
3.  SMB vulnerability investigation.
4.  EternalBlue exploitation.
5.  Malware transfer and execution observation.
6.  Security impact analysis and defensive recommendations.

## 5. Reconnaissance

### 5.1 Objective

The objective was to identify active hosts in the isolated virtual
network and determine which machine should be assessed.

### 5.2 Tool

Nmap.

### 5.3 Recorded command

``` bash
nmap -sn 192.168.91.0/24
```

The `-sn` option performs host discovery without a port scan. The
network range shown is the range recorded in the working notes; 

### 5.4 Results

The host-discovery activity identified active hosts in the virtual
network. The Windows 7 virtual machine was selected as the intended
target.

**Evidence to attach:** `../screenshots/01-host_discovery.png`

## 6. Port and Service Enumeration

### 6.1 Objective

The objective was to identify exposed TCP ports and obtain
service/version information from the verified target.

### 6.2 Recorded command

``` bash
nmap -sV -sC -p- 192.168.91.129
```

  |Option   |Description|
  |-------- |----------------------|
  |`-sV`    |Attempts to identify service versions.|
  |`-sC`    |Runs Nmap's default NSE scripts.|
  |`-p-`   | Scans TCP ports 1--65535.|

### 6.3 Results

The scan output was reviewed to identify exposed services. SMB was
selected for further investigation because it was relevant to the
MS17-010 vulnerability assessment.

**Evidence to attach:** `../screenshots/02-Service_enumeration.png`

## 7. Vulnerability Assessment

### 7.1 Objective

The objective was to investigate the target for known vulnerabilities,
with particular attention to SMB.

### 7.2 Recorded command

``` bash
nmap --script vuln 192.168.91.129
```

The `vuln` script category runs NSE scripts designed to check for known
vulnerabilities. Results are indicators for further investigation and
should not automatically be treated as proof of exploitability.

### 7.3 Vulnerability of interest

  |Attribute                |Details|
  |------------------------| ----------------------|
  |Service                 | SMB|
  |Security bulletin       | MS17-010|
  |Exploitation technique   |EternalBlue|
  |Associated CVE           |CVE-2017-0144|
  |Validation tool          |Metasploit Framework|

MS17-010 is Microsoft's security bulletin covering multiple SMB
vulnerabilities. CVE-2017-0144 is associated with the EternalBlue
vulnerability.

### 7.4 Results

The SMB vulnerability was selected for further validation using
Metasploit. 

**Evidence:**
`../screenshots/03-smb-vulnerability-investigation.png`

## 8. Exploitation -- EternalBlue

### 8.1 Objective

The objective was to validate the selected SMB vulnerability against the
designated Windows 7 lab target.

### 8.2 Tool and module

**Tool:** Metasploit Framework\
**Module:** `exploit/windows/smb/ms17_010_eternalblue`

### 8.3 Results

The EternalBlue module was executed against the lab target. The project
notes and screenshot indicate that exploitation succeeded and a
Metasploit session was established with the Windows 7 machine.

**Evidence** !(../screenshots/07-Execution-attack.png)

## 9. Malware Transfer and Execution

### 9.1 Objective

Following the successful exploitation stage, the exercise examined the
effects of executing a WannaCry malware sample on the isolated Windows 7
target.

### 9.2 Deployment context

The sample was transferred to the target through the established
Metasploit session and executed within the isolated virtual environment.

The malware was not included in the project repository.

### 9.3 Observed results

The project owner reported the following effects after execution:

-   Files were encrypted or became inaccessible.
-   A ransom notification was displayed on the target machine.

**Evidence to attach:** -
`../screenshots/08-malware-execution.png` -
`../screenshots/09-ransom-notification.png` -
`../screenshots/10-before-after-attack.png`

## 10. Analysis and Technical Interpretation

The exercise involved two distinct activities:

1.  **Initial access through exploitation:** EternalBlue was used to
    exploit the selected SMB vulnerability and establish a session with
    the target.
2.  **Subsequent malware execution:** The WannaCry sample was
    transferred and executed through that established session.

WannaCry is known for ransomware behaviour and worm-like propagation
associated with exploitation of vulnerable SMBv1 systems. However, the
lab results documented here establish sample execution and observed
file/ransom effects; they do not independently establish network
propagation by the sample.

The distinction is important when interpreting the results and
presenting the project in a technical interview.

## 11. Security Impact

The observed file encryption or inaccessibility demonstrates an impact
on the availability of data in the test environment.

  |Security property  | Assessment|
  |---------- |-----------------------------------|
  |Confidentiality    |   Data theft or exfiltration was not verified in this exercise.|
  |Integrity   |  File contents or accessibility were affected; exact changes should be   supported by evidence.|
  |Availability     | Access to affected files was disrupted.|

Potential real-world consequences of ransomware incidents can include
operational disruption, recovery costs, loss of access to important
data, and broader organizational impact.

## 12. Detection Opportunities for SOC Analysts

The following are useful detection areas for a defensive monitoring
exercise. They are recommended investigation points, not detections
confirmed as performed in this project.

  |Area      |Activity to investigate|
  |-------------|-----------------|
  |SMB network activity     |Unexpected or unusual connections   involving TCP port 445|
  |Process activity     |Unexpected executable launches and suspicious process behaviour|
  |File activity     | A high volume of unusual file modifications or renames|
  |Ransomware indicators    | Ransom notes, unusual extensions, or files becoming inaccessible|
  |Endpoint security    | Antivirus/EDR alerts and suspicious execution events|

## 13. Incident Response Recommendations

### 13.1 Identification

-   Review endpoint alerts and suspicious process activity.
-   Investigate unusual SMB connections.
-   Identify affected systems and the scope of file changes.
-   Preserve relevant logs and evidence.

### 13.2 Containment

-   Isolate affected endpoints from the network.
-   Prevent further communication with potentially affected systems.
-   Preserve evidence before destructive remediation where practical.

### 13.3 Eradication

-   Identify and remove malicious components through a controlled
    remediation process.
-   Address the exploited vulnerability.
-   Rebuild affected systems where integrity cannot be trusted.
-   Verify the system is clean before restoring connectivity.

### 13.4 Recovery

-   Restore data from verified clean backups.
-   Validate restored systems and data.
-   Monitor for recurring suspicious activity.
-   Document lessons learned.

These are recommended response procedures. The project did not establish
that a complete incident-response lifecycle was carried out.

## 14. Remediation and Prevention

-   Apply the security updates associated with MS17-010.
-   Disable SMBv1 where it is not required.
-   Restrict SMB exposure using host and network controls.
-   Segment networks to limit lateral movement.
-   Use supported operating systems.
-   Deploy and maintain endpoint protection.
-   Restrict unauthorized executable execution.
-   Maintain offline or otherwise isolated backups.
-   Test backup restoration and incident-response procedures.
-   Monitor suspicious process, network, and file activity.

## 15. Limitations

-   The assessment was performed in a virtual lab and does not represent
    a production penetration test.
-   The target IP address must be reconciled against the original
    host-discovery, Nmap, and Metasploit evidence.
-   The exact privilege level of the Metasploit session has not been
    established in this report.
-   The exact scope of file encryption or inaccessibility requires
    supporting evidence.
-   Network propagation by the WannaCry sample was not independently
    verified.
-   Data exfiltration, persistence, and a complete forensic examination
    were not established.
-   Detection engineering and a full incident-response lifecycle are
    recommendations for future work, not completed project results.

## 16. Conclusion

This project provided practical exposure to SMB vulnerability
investigation, EternalBlue exploitation, and ransomware execution in an
isolated virtual environment.

Nmap was used for reconnaissance and vulnerability investigation.
Metasploit was then used to validate the selected SMB vulnerability, and
a session with the Windows 7 target was reported as successfully
established.

The WannaCry sample was subsequently transferred and executed through
that session. The reported effects included file encryption or
inaccessibility and a ransom notification.

The exercise highlights the importance of patch management, reducing
unnecessary SMB exposure, endpoint security, network segmentation,
reliable backups, and structured incident response. It also provides a
foundation for further SOC-focused work involving endpoint telemetry,
log analysis, and ransomware detection.

## 17. Disclaimer

This exercise was conducted for educational purposes in an isolated
virtual lab. An actual WannaCry sample was used during the experiment;
the sample and any malware payloads are not included in this repository.
The project documentation is not an instruction to obtain, distribute,
or execute malware. Do not run malware on a personal host, production
system, or network without explicit authorization and appropriate
containment.

## 18. References

-   [Microsoft Security Bulletin
    MS17-010](https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
-   [Nmap Reference Guide](https://nmap.org/book/man.html)
