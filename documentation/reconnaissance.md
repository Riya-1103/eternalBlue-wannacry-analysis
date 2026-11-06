## Objective
The first step was to identify active hosts within the virtual lab network.
Nmap was used to discover available hosts within the subnet.
### Command Executed
```bash
nmap -sn 192.168.91.0/24
```
### Command Explanation
•	nmap: Network scanning tool.
•	-sn: Performs host discovery without conducting a port scan.
•	192.168.91.0/24: Specifies the network range to investigate.

## Observation
The scan identified active hosts within the virtual network. The Windows 7 machine was selected as the target for further assessment.
Evidence:

## Port and Service Scanning
### Objective
After identifying the target, a detailed port scan was performed to discover open ports and identify running services and their versions.
Command Executed
```bash
nmap -sV -sC -p- 192.168.91.129
```
### Command Explanation
|Option |	Description |
| ----- | ------- |
|-sV	|Detects service versions.|
|-sC	|Runs Nmap's default NSE scripts.|
|-p- 	|Scans all TCP ports from 1 to 65535.|

### Observation
The scan results were examined to identify exposed services and potential entry points.
The SMB service was selected for further investigation because it was relevant to the MS17-010 vulnerability assessment.
Evidence: 
