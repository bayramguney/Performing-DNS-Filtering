# Performing-DNS-Filtering

# 🌐 Assisted Lab: Performing DNS Filtering

## 📌 Overview

This lab demonstrates how to investigate suspicious DNS activity, identify Indicators of Compromise (IoCs), automate DNS filtering using threat intelligence, and perform DNS reconnaissance using **nslookup** and **dig**.

You begin by analyzing DNS client logs for suspicious behavior, identify beaconing to a malicious domain, create an automated DNS blocking script, and perform DNS enumeration against a public domain.

> **Note:** The domain **comptia.org** is used only for educational purposes in this lab. It is **not** considered malicious.

---

## 🎯 Objectives

This lab aligns with the following **CompTIA Security+ (SY0-701)** objectives:

- **2.4** – Analyze indicators of malicious activity
- **4.4** – Explain security alerting and monitoring concepts
- **4.5** – Modify enterprise capabilities to enhance security
- **4.7** – Explain automation and orchestration in secure operations
- **4.9** – Use data sources to support an investigation

---

# 🖥️ Lab Environment

| System | Purpose |
|---------|----------|
| PC10 | Windows Server 2019 Client |
| Kali Linux | Security workstation |
| Event Viewer | DNS event investigation |
| Windows PowerShell | Generate DNS activity |
| Bash | Automation scripting |
| Cron | Task scheduling |
| nslookup | DNS reconnaissance |
| dig | Advanced DNS queries |

---

# 🛠️ Technologies Used

- DNS Client Logging
- Windows Event Viewer
- PowerShell
- Bash
- Cron
- Linux `/etc/hosts`
- curl
- nslookup
- dig
- Threat Intelligence Feed
- DNS Filtering
- DNS Reconnaissance

---

# 📚 Skills Learned

- DNS threat hunting
- Indicator of Compromise (IoC) identification
- DNS log analysis
- Detecting beaconing behavior
- Threat intelligence integration
- DNS filtering
- Bash scripting
- Linux hosts file management
- Automation with Cron
- DNS reconnaissance
- SOA, NS, MX, A, AAAA, and CNAME record analysis
- Using nslookup
- Using dig
- Defensive security automation

---

# 🚨 Scenario

Structureality Inc.'s ISP reported suspicious outbound DNS activity originating from an internal workstation.

As a security analyst, your objectives are to:

- Investigate DNS client logs
- Identify suspicious domain requests
- Detect malware beaconing
- Block malicious domains automatically
- Perform DNS reconnaissance for further analysis

---

# 🔍 Part 1 – Investigating DNS Activity

DNS Client logging was enabled on **PC10** using Event Viewer.

Actions performed:

- Enabled DNS Client Operational logging
- Generated simulated DNS traffic
- Filtered logs by Event ID **3010**
- Reviewed DNS query events
- Identified suspicious Fully Qualified Domain Names (FQDNs)

### Investigation Findings

A suspicious domain was repeatedly queried:

- **badsite.ru**

Additional observations:

- Continuous DNS requests
- Repeated A and AAAA lookups
- Queries occurring at regular intervals
- DNS activity originated from the same process

---

# 🚨 Beaconing Detection

The repeated DNS requests occurred approximately every **20 seconds**, indicating **DNS beaconing**.

Beaconing is commonly associated with:

- Malware
- Botnets
- Command-and-Control (C2) communications
- Persistent attacker connectivity

The investigation also identified the Process ID responsible for generating the DNS requests, providing valuable information for malware analysis.

---

# 🤖 Part 2 – Automating DNS Filtering

To prevent systems from resolving known malicious domains, a Bash script was created.

The script:

- Downloads a DNS threat feed
- Reads each malicious domain
- Adds entries to `/etc/hosts`
- Redirects malicious domains to `127.0.0.1`
- Removes duplicate entries

### Script Workflow

1. Retrieve threat feed
2. Read malicious domains
3. Update `/etc/hosts`
4. Redirect domains to localhost
5. Remove duplicate entries

---

# 🔐 DNS Blocking

After running the automation script:

- Malicious domains resolved to **127.0.0.1**
- DNS lookups were effectively blocked
- Connections to malicious websites failed
- Systems remained protected even without modifying the DNS server

This demonstrates a simple but effective proof-of-concept DNS filtering solution.

---

# ⏰ Scheduled Automation

To keep threat intelligence current, the script was scheduled using **Cron**.

Schedule:

- Daily
- **03:00 AM**

This allows automatic updates to the local DNS block list without manual intervention.

---

# 🔎 Part 3 – DNS Reconnaissance with nslookup

The **nslookup** utility was used to investigate DNS information for **comptia.org**.

Queries performed included:

- Default DNS server
- A records
- SOA records
- NS records
- MX records
- CNAME records

Information gathered included:

- Authoritative DNS server
- Mail server information
- Nameservers
- IP addresses
- Domain aliases

The investigation also demonstrated the difference between:

- Cached (Non-authoritative) responses
- Authoritative DNS responses

---

# 🔍 Part 4 – DNS Reconnaissance with dig

The **dig** utility was used to perform the same investigation with more detailed output.

Resource records queried included:

- SOA
- A
- NS
- MX
- CNAME

Unlike nslookup, **dig** provides:

- Detailed DNS responses
- Better formatting
- Easier automation
- More useful output for security reports

---

# 📖 DNS Record Types Reviewed

| Record | Purpose |
|---------|----------|
| A | IPv4 address |
| AAAA | IPv6 address |
| SOA | Start of Authority |
| NS | Name Server |
| MX | Mail Server |
| CNAME | Canonical Name (Alias) |

---

# 🛡️ Security Benefits

DNS filtering helps organizations:

- Block malware communications
- Prevent phishing access
- Stop Command-and-Control traffic
- Reduce ransomware infections
- Prevent access to malicious websites
- Improve endpoint protection

Automation ensures protection remains up to date as new malicious domains are discovered.

---

# 📖 Key Takeaways

This lab demonstrated how security analysts can investigate suspicious DNS activity, detect beaconing behavior, automate DNS filtering using threat intelligence, and perform DNS reconnaissance using industry-standard tools.

By combining **Windows Event Viewer**, **PowerShell**, **Bash**, **Cron**, **nslookup**, and **dig**, organizations can proactively identify malicious activity and strengthen DNS security.

---

# 🏷️ Tags

`CompTIA Security+` `DNS Filtering` `Threat Hunting` `Threat Intelligence` `Beaconing` `Indicator of Compromise` `Windows Event Viewer` `PowerShell` `Linux` `Bash` `Cron` `Automation` `DNS Security` `nslookup` `dig` `Blue Team` `SOC Analyst` `Cybersecurity Lab`
