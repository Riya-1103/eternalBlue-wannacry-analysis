## Incident Response and Mitigation
A ransomware incident requires a structured response to minimize damage and restore normal operations.
## Detection
SOC analysts should investigate:
•	Unusual SMB connections.
•	Suspicious executable activity.
•	Unexpected file modifications.
•	Unusual file extensions.
•	Ransom notifications.
•	Endpoint security alerts.
## Containment
•	Immediately isolate affected systems from the network.
•	Prevent communication with other potentially vulnerable systems.
•	Preserve relevant logs and forensic evidence.
•	Avoid reconnecting compromised systems before investigation.
## Eradication
•	Identify and remove the malicious software through a controlled remediation process.
•	Investigate the initial entry point.
•	Apply the relevant security patches.
•	Verify that the compromised system is clean.
## Recovery
•	Restore affected data from verified clean backups.
•	Rebuild compromised systems when necessary.
•	Verify system integrity before restoring network connectivity.
•	Monitor systems for signs of reinfection.
## Preventive Measures
•	Apply MS17-010 security updates.
•	Disable SMBv1 where it is not required.
•	Implement network segmentation.
•	Use updated endpoint detection and protection solutions.
•	Restrict unauthorized executable execution.
•	Maintain offline or isolated backups.
•	Conduct regular vulnerability assessments.


