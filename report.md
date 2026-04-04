# Windows Sysmon + Active Directory Incident Investigation Report

## Executive Summary
This investigation reviewed suspicious activity on a Windows 11 host. Multiple failed logon attempts were detected, followed by a successful login, then by PowerShell activity within the same user instance. Windows Security logs and Sysmon logs were reviewed in Splunk to confirm processes and document the activity.

## Incident Overview
- The incident took place on **April 2, 2026**, on the host **ARROYOBOYO,** a domain-connected Windows 11 host in the **ArroyoAD** environment.
- Affected account was a newly created domain user named “victim.” The investigation used evidence sourced from Windows login activity, PowerShell execution on the endpoint, and Splunk log analysis.
- The main entities involved were the victim user account, the monitored Windows endpoint, Sysmon process creation logs, and the analyst conducting the review.

## Detection and Analysis
The incident was first noticed via a custom Splunk dashboard named “Windows Access Security Monitoring” that was made in a previous lab.

<img width="1633" height="1067" alt="07-Suspicous-logon-activity-detected" src="https://github.com/user-attachments/assets/4bf5cad6-814f-40da-9548-4123d2b7ac16" />

Further investigation found a spike in failed logon attempts tied exclusively to the user ‘victim,’ signs of targeted authentication attack behavior (T1110.001). Via log analysis, **5 EventCode 4625 logs** were discovered in rapid succession from **10:27:57 PM** to **10:28:02 PM,** followed shortly by a successful authentication shown by **EventCode 4624** at **10:28:09 PM.**

<img width="803" height="649" alt="08-victim-user-identification" src="https://github.com/user-attachments/assets/75cf0c38-9237-499f-840c-dabafd142c4d" />
<img width="674" height="642" alt="09-first-failed-login-attempt" src="https://github.com/user-attachments/assets/6d364d88-9d78-4309-954f-14d8830dcf55" />
<img width="1136" height="474" alt="10-first-successful-login-attempt" src="https://github.com/user-attachments/assets/0080646b-d744-45e5-a997-15389df825e5" />

**Sysmon EventID 1 events** confirmed PowerShell execution under user ‘victim’ immediately after authentication at **10:28:28 PM.** Command-line evidence showed use of **whoami**, **whoami /priv,** **ipconfig /all,** and **net user.** The combination of repeated failed logons, successful access, and then immediate command execution was deemed suspicious and consistent with possible account misuse and system reconnaissance attempts.

<img width="1621" height="1080" alt="11-rapid-process-alerts-login-attempts" src="https://github.com/user-attachments/assets/29a48c5a-2226-4d6e-8f30-654d958ae333" />
<img width="1201" height="732" alt="12-powershell-usage-proof" src="https://github.com/user-attachments/assets/b26b22fc-1dd5-4c80-8524-f4936da681ad" />
<img width="1137" height="752" alt="13-more-powershell-process-proof" src="https://github.com/user-attachments/assets/46a958ff-f445-40c7-a8b7-90486b3bea72" />
<img width="1267" height="985" alt="14-first-powershell-usage-attempt" src="https://github.com/user-attachments/assets/1eb093a5-0178-4cbb-970b-56ff2cb67076" />
<img width="1133" height="919" alt="15-specific-commands-used-proof" src="https://github.com/user-attachments/assets/ea4a806e-74ad-4f8b-b5e1-f0b619aa9211" />

## Containment, Eradication, and Recovery
Because this was a controlled lab investigation, no live containment actions were taken. In a real environment, I would recommend that containment actions be taken immediately. This includes separating the workstation from the network and other devices to mitigate exposure. Eradication would focus on removing unauthorized access and reviewing the host for additional suspicious activity like C2 connection attempts. Recovery actions would include returning the system to normal, confirming account security and integrity across files and functions, and increasing monitoring for similar behavior.

## Post-Incident (Lessons Learned)
This project shows how Windows Security logs combined with Sysmon process creation events could build a full incident timeline. The spike in failed logons alone showed suspicious activity, but Sysmon provided the evidence needed to confirm what happened immediately after login. Post-incident recommendations include reviewing the affected account, improving alerting for rapid failed logon patterns, expanding PowerShell visibility and controls, tightening privilege and access management, and validating stronger endpoint hardening for authentication and command-line activity.

## Supporting Evidence / Documentation
Supporting evidence includes screenshots showing the creation of the victim user in Active Directory, successful domain login by the victim user, PowerShell command execution on the Windows 11 host, failed logon events in Splunk, successful logon events in Splunk, Sysmon process creation activity, and proof of command-line execution. Key evidence included EventCode 4625 for failed logons, EventCode 4624 for successful logons, and Sysmon EventID 1 for PowerShell-related process creation and specific command usage, including whoami, whoami /priv, ipconfig /all, and net user.

<img width="945" height="766" alt="01-creating-victim-user-AD" src="https://github.com/user-attachments/assets/9e62efde-36c4-4155-b869-77e10c658307" />
<img width="951" height="766" alt="02-new-user-confirmation" src="https://github.com/user-attachments/assets/88408a79-b1f6-4de9-a0ad-5c6197c97aaf" />
<img width="1627" height="1148" alt="03-vitcim-login-attempts" src="https://github.com/user-attachments/assets/101287ce-ffe1-4cf6-a69d-34c9b19d3afa" />
<img width="1278" height="746" alt="05-victim-powershell commands-1" src="https://github.com/user-attachments/assets/8086c20d-1f62-4916-9010-5e585570a4cc" />
<img width="1277" height="778" alt="06-victim-powershell commands-2" src="https://github.com/user-attachments/assets/93ea62b3-8f94-4308-a546-935e645dd87b" />



