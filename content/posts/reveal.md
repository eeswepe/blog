+++
date = '2025-04-15T12:27:29+07:00'
draft = false
title = 'Reveal'
tags = ['cyberdefenders', 'memory dump', 'volatility', 'forensics']
+++

# Reveal
![challenge banner](/img/reveal/banner.png)

Link: [https://cyberdefenders.org/blueteam-ctf-challenges/reveal/](https://cyberdefenders.org/blueteam-ctf-challenges/reveal/)

## Scenario
You are a forensic investigator at a financial institution, and your SIEM flagged unusual activity on a workstation with access to sensitive financial data. Suspecting a breach, you received a memory dump from the compromised machine. Your task is to analyze the memory for signs of compromise, trace the anomaly's origin, and assess its scope to contain the incident effectively.

## File Analysis
given zip file. the zip file contains memory dump of the machine.

## Questions

### 1. Identifying the name of the malicious process helps in understanding the nature of the attack. What is the name of the malicious process?

By using `vol -f 192-Reveal.dmp windows.pslist` command, we can find the name of the malicious process.

![pslist](/img/reveal/q1.png)

**Answer:** **powershell.exe**

---

### 2. Knowing the parent process ID (PPID) of the malicious process aids in tracing the process hierarchy and understanding the attack flow. What is the parent PID of the malicious process?

By using `vol -f 192-Reveal.dmp windows.pslist` command, we can find the parent PID of the malicious process.

![pslist](/img/reveal/q1.png)

**Answer: 4120**

---

### 3. Determining the file name used by the malware for executing the second-stage payload is crucial for identifying subsequent malicious activities. What is the file name that the malware uses to execute the second-stage payload?

By using `vol -f 192-Reveal.dmp windows.cmdline` command, we can find the command line of the malicious process. wee can see that the malware use net command to get malicious dll file on shared directory then execute it with rundll32.

![cmdline](/img/reveal/q3.png)

**Answer: 3435.dll**

---

### 4. Identifying the shared directory on the remote server helps trace the resources targeted by the attacker. What is the name of the shared directory being accessed on the remote server?

from that picture we can see that the shared directory is `davwwwroot`

**Answer: davwwwroot**

---

### 5. What is the MITRE ATT&CK sub-technique ID that describes the execution of a second-stage payload using a Windows utility to run the malicious file?

by ssearching through goolge, i got a great article that talk about rundll32 and mitre att&ck. [here](https://d3fend.mitre.org/offensive-technique/attack/T1218.011/)

**Answer: T1218.011**

---

### 6. Identifying the username under which the malicious process runs helps in assessing the compromised account and its potential impact. What is the username that the malicious process runs under?

By using `vol -f 192-Reveal.dmp windows.sessions` command, we can find the username of the malicious process.

![sessions](/img/reveal/q6.png)

**Answer: Elon**

---

### 7. Knowing the name of the malware family is essential for correlating the attack with known threats and developing appropriate defenses. What is the name of the malware family?

Actually i don't know the name of the malware family because i done this labs after when this lab was retired. but i read on some writeup [(here)](https://medium.com/@chaoskist/cyberdefenders-write-up-reveal-3a318ca0f603) and i get the name of the malware family is "STRELASTEALER"

**Answer: STRELASTEALER**
