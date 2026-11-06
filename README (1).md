# EternalBlue Exploitation and WannaCry Ransomware Analysis

A controlled virtual-lab project exploring SMB vulnerability assessment,
EternalBlue exploitation, and the observed impact of a WannaCry malware
sample on a Windows 7 test machine.

> **Safety notice:** This repository contains documentation and
> sanitized evidence only. It does not contain the WannaCry executable,
> malware payloads, or instructions for obtaining or deploying malware.
> The malware sample was handled in an isolated virtual environment for
> educational analysis.

## Project Overview

This project documents a practical cybersecurity exercise using Kali
Linux as the attacker machine and Windows 7 as the target machine in
VMware. Nmap was used for reconnaissance and vulnerability
investigation. Metasploit's EternalBlue module was then used to exploit
the SMB vulnerability associated with Microsoft's MS17-010 security
bulletin.

After a Metasploit session was established, an actual WannaCry malware
sample was transferred and executed on the isolated Windows 7 virtual
machine. The reported observations were file encryption or
inaccessibility and the display of a ransom notification.

**Important distinction:** The project demonstrates EternalBlue
exploitation followed by malware execution through the established
session. It does not, based on the evidence currently documented,
establish that WannaCry propagated through SMB during this experiment.

## Objectives

-   Discover active hosts and exposed services in the virtual lab.
-   Investigate the target's SMB service for the vulnerability
    associated with MS17-010.
-   Validate the selected vulnerability using Metasploit in the
    authorized lab.
-   Document the subsequent malware execution and observed effects.
-   Identify relevant defensive monitoring and incident-response
    considerations.
-   Produce a clear technical assessment with evidence and remediation
    recommendations.

## Lab Environment

  Component                 Details
  ------------------------- ------------------------------------
  Virtualization            VMware Workstation
  Attacker                  Kali Linux
  Target                    Windows 7 virtual machine
  Reconnaissance            Nmap
  Exploitation framework    Metasploit Framework
  Exploitation technique    EternalBlue
  Vulnerability reference   MS17-010; associated CVE-2017-0144
  Malware analysed          WannaCry sample
  Network                   Isolated virtual lab

### Network addressing

The working notes have referenced Kali as `192.168.91.128` and Windows 7
as `192.168.91.129`, while a host-discovery note also mentioned
`192.168.91.130`. Confirm the final addresses from the original
screenshots or lab records before publishing. Do not assume that `.130`
is the target.

## Methodology

1.  **Reconnaissance:** Identify active hosts in the isolated lab
    network.
2.  **Port and service enumeration:** Examine exposed TCP services and
    versions on the verified Windows 7 target.
3.  **Vulnerability investigation:** Investigate the SMB service and the
    MS17-010 vulnerability candidate.
4.  **Exploitation:** Use the Metasploit EternalBlue module in the
    authorized lab and record the actual session result.
5.  **Malware execution observation:** Document the sample execution
    performed through the established session and the effects observed
    on the target.
6.  **Security analysis:** Discuss detection opportunities, containment,
    eradication, recovery, and preventive controls.

## Key Results

-   Nmap was used for host discovery, service enumeration, and
    vulnerability investigation.
-   The EternalBlue module was reported to have successfully established
    a session with the Windows 7 target.
-   The WannaCry sample was transferred and executed through that
    session.
-   The reported effects were file encryption or inaccessibility and a
    ransom notification.
-   Network propagation was not independently verified and is not
    claimed as a project result.

The final report should be read for the detailed methodology,
limitations, evidence, and recommendations.

## Repository Structure

``` text
eternalblue-wannacry-analysis/
│
├── README.md
├── documentation/
│   ├── lab-setup.md
│   ├── reconnaissance.md
│   ├── vulnerability-assessment.md
│   └── exploitation.md
├── malware-analysis/
│   ├── sample-information.md
│   ├── execution-observations.md
│   └── behaviour-analysis.md
├── detection/
│   └── detection-opportunities.md
├── incident-response/
│   └── response-and-mitigation.md
├── screenshots/
│   └── [sanitized evidence images]
└── report/
    └── final-assessment.md
```

## Evidence

Add only sanitized screenshots that support the statements in the
report. Suggested filenames:

-   `01-host-discovery.png`
-   `02-service-enumeration.png`
-   `03-smb-vulnerability-investigation.png`
-   `04-eternalblue-session.png`
-   `05-malware-execution-observation.png`
-   `06-ransom-notification.png`
-   `07-file-state-before-after.png`

Do not upload the malware sample, executable payloads, credentials,
private keys, or sensitive host information.

## Limitations

-   The experiment was performed against a lab virtual machine, not a
    production environment.
-   The precise target IP must be reconciled against the original
    evidence before publication.
-   The exact privilege level of the established session should only be
    stated if it was verified.
-   File encryption or inaccessibility and a ransom notification were
    reported; the precise file-level effects should be supported by
    screenshots or other evidence.
-   WannaCry's worm-like SMB propagation was not independently
    demonstrated in this exercise.
-   This project does not claim a complete forensic examination,
    persistence analysis, data-exfiltration analysis, or full
    incident-response execution.

## Security and Ethical Disclaimer

This work was performed for educational purposes in an isolated virtual
lab under the project owner's control. Do not run malware on a host
operating system, a production network, or any system without explicit
authorization. Revert the affected virtual machine to a known-clean
snapshot or rebuild it before any further use. This repository
intentionally excludes the malware sample and operational payloads.

## References

-   [Microsoft Security Bulletin
    MS17-010](https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
-   [Nmap Reference Guide](https://nmap.org/book/man.html)
-   [MITRE ATT&CK](https://attack.mitre.org/)

## Author

Add your name, GitHub profile, and contact details here if you want them
publicly visible.
