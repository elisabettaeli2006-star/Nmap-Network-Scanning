# Nmap-Network-Scanning

# Network Vulnerability Scanning (Reconnaissance)

## Overview
This project focuses on the reconnaissance phase of a penetration test. The objective is to map a target system on a local network, identify its IP address, bypass basic host-based firewall protections, and discover open ports and active services using **Nmap**.

## Environment & Tools
* **Attacker Machine:** Kali Linux (VirtualBox)
* **Target Machine:** Windows 11 Enterprise (VirtualBox)
* **Network:** Custom NAT Network (`NatNetwork`)
* **Core Tool Used:** Nmap (Network Mapper)

## Execution Steps

### 1. Target Identification & Firewall Evasion
Initially, the Windows 11 machine had its Windows Defender Firewall active. A standard Nmap scan returned `1000 filtered tcp ports`, indicating that the firewall was silently dropping the probes. 
To simulate a vulnerable environment or an internal network scenario where firewalls might be misconfigured, the Windows Defender Firewall was intentionally disabled across all network profiles.

### 2. Network Scanning
Once the target's IP address (`10.0.2.3`) was confirmed via the `ipconfig` command on the host, a service version scan was executed from Kali Linux to identify specific listening ports.

**Command Used:**
`nmap -sV 10.0.2.3`
*(Note: `-sV` flag is used to determine the version of the services running on the open ports).*

## Findings & Results
The scan successfully bypassed the network defenses and identified **3 open ports** on the Windows 11 target:

* **Port 135/tcp (msrpc):** Microsoft Remote Procedure Call.
* **Port 139/tcp (netbios-ssn):** NetBIOS Session Service, historically used for file and printer sharing.
* **Port 445/tcp (microsoft-ds):** Server Message Block (SMB). This is a critical port often targeted by attackers for exploitation (e.g., EternalBlue/WannaCry) to gain unauthorized access or execute remote code.

> **Proof of Execution:**
![Nmap Scan Results](./Pictures/Screenshots/nmaptest)

## 💡 Conclusion
This lab demonstrates the fundamental process of network discovery. Identifying exposed services like SMB (Port 445) provides the necessary blueprint for the next phases of a penetration test, such as vulnerability analysis and exploitation.
