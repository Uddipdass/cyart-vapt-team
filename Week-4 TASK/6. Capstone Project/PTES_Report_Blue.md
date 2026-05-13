---
PTES Penetration Test Report
Title: HackTheBox Blue
---

## Executive Summary

A full penetration test was conducted against the HackTheBox Blue machine (192.168.1.10) following the Penetration Testing Execution Standard framework. The target was identified as a Windows 7 Professional SP1 system running an unpatched SMBv1 service.

Exploitation of CVE-2017-0143, commonly known as EternalBlue, resulted in complete administrative compromise of the target with no credentials required. A Meterpreter session running as NT AUTHORITY\SYSTEM was established, granting unrestricted access to all files, credentials, and system resources.

The overall risk rating for this engagement is Critical with a CVSS score of 9.3.

---

## Attack Timeline

The engagement began with active reconnaissance using Nmap, which identified open SMB ports on 139 and 445 and fingerprinted the operating system as Windows 7 SP1. A targeted Nmap vulnerability script confirmed the presence of MS17-010. OpenVAS was subsequently run to corroborate the finding and produce a full vulnerability inventory of the host.

Metasploit's ms17_010_eternalblue module was launched against the target. Within seconds, a Meterpreter reverse shell was returned running as NT AUTHORITY\SYSTEM. Post-exploitation activities included system enumeration, password hash extraction via hashdump, and capture of both user and administrator flags confirming full system compromise.

---

## Remediation Plan

Three actions are required immediately.

First, apply Microsoft security patch MS17-010 (KB4012212) to all affected Windows systems without delay.

Second, disable the SMBv1 protocol across the network using Group Policy or PowerShell, as this protocol is deprecated and no longer necessary in any modern environment.

Third, block SMB ports 139 and 445 at the network perimeter firewall to prevent external exposure. Additionally, a formal patch management policy enforcing a 48-hour critical patch window should be established, and an OpenVAS rescan should be conducted after remediation to verify all vulnerabilities have been resolved.
