+++
date = '2025-04-15T18:26:39+07:00'
draft = false
title = 'Red Stealer'
tags = ['forensics', 'VirusTotal', 'MalwareBazaar', 'ThreatFox', 'cyberdefenders']
+++

# Red Stealer

![redstealer](/img/red-stealer/banner.png)

Link: [https://cyberdefenders.org/blueteam-ctf-challenges/red-stealer/](https://cyberdefenders.org/blueteam-ctf-challenges/red-stealer/)

---

## Scenario

You are part of the Threat Intelligence team in the SOC (Security Operations Center). An executable file has been discovered on a colleague's computer, and it's suspected to be linked to a Command and Control (C2) server, indicating a potential malware infection.Your task is to investigate this executable by analyzing its hash. The goal is to gather and analyze data beneficial to other SOC members, including the Incident Response team, to respond to this suspicious behavior efficiently.

## File Analysis

---

Given zip file containing txt files with the following information:

```
File Hash (SHA-256): 248FCC901AFF4E4B4C48C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B

Use this hash on online threat intel platforms (e.g., VirusTotal, Hybrid Analysis) to complete the lab analysis
```

---

## Questions

### 1. Categorizing malware enables a quicker and clearer understanding of its unique behaviors and attack vectors. What category has Microsoft identified for that malware in VirusTotal?

By Search the sha256 hash on [virustotal](https://www.virustotal.com/gui/file/248FCC901AFF4E4B4C48C91E4D78A939BF681C9A1BC24ADDC3551B32768F907B) i get the category of the malware on popular threat label section which is "trojan"

![virustotal](/img/red-stealer/q1.png)

**Answer: trojan**

### 2. Clearly identifying the name of the malware file improves communication among the SOC team. What is the file name associated with this malware?

By visiting Details page on virustotal, i get a lot of file name, but only "Wextract" is the suitable file name for the submit form.

![virustotal](/img/red-stealer/q2.png)

**Answer: Wextract**

### 3. Knowing the exact timestamp of when the malware was first observed can help prioritize response actions. Newly detected malware may require urgent containment and eradication compared to older, well-documented threats. What is the UTC timestamp of the malware's first submission to VirusTotal?

By visiting Details page on virustotal, i get the timestamp of the first submission report for the malware which is 2023-10-06 04:41:50 UTC.

![virustotal](/img/red-stealer/q3.png)

**Answer: 2023-10-06 04:41**

### 4. Understanding the techniques used by malware helps in strategic security planning. What is the MITRE ATT&CK technique ID for the malware's data collection from the system before exfiltration?

By visiting Behavior page, i searched for collection and i get the id for the technique which is T1005

![virustotal](/img/red-stealer/q4.png)

**Answer: T1005**

### 5. Following execution, which social media-related domain names did the malware resolve via DNS queries?

By visiting Behavior page, if we look into http requests section we get several url and www.facebook.com is the only one which social media platforms.

![virustotal](/img/red-stealer/q5.png)

**Answer: www.facebook.com**

### 6. Once the malicious IP addresses are identified, network security devices such as firewalls can be configured to block traffic to and from these addresses. Can you provide the IP address and destination port the malware communicates with?

By visiting Behavior page, if we look into memory pattern urls section we got several ip address and destination port.but the first one was suspicious because it has no DNS.

![virustotal](/img/red-stealer/q6.png)

**Answer: 77.91.124.55:19071**

### 7. YARA rules are designed to identify specific malware patterns and behaviors. Using MalwareBazaar, what's the name of the YARA rule created by "Varp0s" that detects the identified malware?

As the instructions. i go to MalwareBazaar and search for the sha256 and i got just 1 result. And if we click into the sha256 text, we will directed into the 'information' page.

![virustotal](/img/red-stealer/q7-1.png)

and if we click the YARA (as the instructions). we will get several rule name, but only detect_Redline_Stealer is the suitable one(authored by Varp0s).

![virustotal](/img/red-stealer/q7-2.png)

**Answer: detect_Redline_Stealer**

### 8. Understanding which malware families are targeting the organization helps in strategic security planning for the future and prioritizing resources based on the threat. Can you provide the different malware alias associated with the malicious IP address according to ThreatFox?

Because ThreatFox doesnt support for sha256 search. i will use malware family instead. So, i search for the malware family and i get "Redline". After that lets search that malware family at ThreatFox. 

![virustotal](/img/red-stealer/q8-1.png)

by clicking the redline stealer, we will get the different malware alias which is RECORDSTEALER.

![virustotal](/img/red-stealer/q8-2.png)

**Answer: RECORDSTEALER**

### 9. By identifying the malware's imported DLLs, we can configure security tools to monitor for the loading or unusual usage of these specific DLLs. Can you provide the DLL utilized by the malware for privilege escalation?

Back into virustotal and click on Behavior, if we look at modules loaded. there is several modules. but advapi was suspicious for me because it can handle some advanced windows function

![virustotal](/img/red-stealer/q9.png)

**Answer: advapi32.dll**
