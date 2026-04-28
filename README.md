# C844 – Emerging Technologies in Cybersecurity (WGU)

**Student:** Sara Goodie  
**Course:** C844 – Emerging Technologies in Cybersecurity  
**Program:** Western Governors University

---

## Repository Contents

| File | Description |
|------|-------------|
| `Task1_SaraGoodie_R_C844.docx` | **Task 1** – Network Mapping and Monitoring (Nmap + Wireshark lab) |
| `Sara_Goodie_Task2C844.pdf` | **Task 2** – WLAN and Mobile Security Plan (Alliah scenario) |

---

## Task 1 – Network Mapping and Monitoring

A hands-on lab using **Nmap** and **Wireshark** to scan, analyze, and identify vulnerabilities across a target network (`10.168.27.0/24`).

### Network Topology

- **Identified topology:** Star topology
- All devices connect to a central localhost (hub/switch)
- Advantage: single device failure does not bring down the network
- Weakness: if the central localhost fails, all connected devices go down; redundancy requires additional hardware

### Nmap Vulnerabilities Found

| Device IP | Vulnerability | Risk |
|-----------|--------------|------|
| `10.168.27.10` | Open ports: HTTP (80), FTP (21) | Unauthorized access vectors |
| `10.168.27.15` | Outdated OS: Windows 8.1 (EOL Jan 2023) | Unpatched security flaws, no Microsoft support |
| `10.168.27.14` | High uptime: 17,248,638 seconds | Delayed patches, memory leaks, resource exhaustion |

### Wireshark Anomalies Found

| Frame | Anomaly | Potential Implication |
|-------|---------|----------------------|
| Frame 15760 | DCERPC TCP Spurious Retransmission | Network congestion, packet loss, delayed ACKs |
| Frame 85 | TCP ACKed Unseen Segment | Possible man-in-the-middle (MITM) attack; lost/altered segments |
| Frame 1615 | HTTP cleartext credential exposure | Full username and password visible in plaintext; confidentiality breach |

### Solution Recommendations

**Nmap fixes:**
- Close port 80 (HTTP) → enable port 443 (HTTPS) for encrypted browser-to-server communication
- Close port 21 (FTP) → enable port 22 (SFTP) for secure file transfer
- Upgrade Windows 8.1 → Windows 11 (current supported release)
- Schedule automatic restarts to ensure timely security and hardware updates and reduce high uptime risks

**Wireshark fixes:**
- Spurious Retransmissions → analyze TCP SACK (selective acknowledgement); adjust retransmission timers
- TCP ACKed Unseen Segment (MITM risk) → implement HTTPS, VPN, antivirus, and IDPS (Intrusion Detection and Prevention Systems)
- HTTP credential exposure → close port 80, enable HTTPS port 443

---

## Task 2 – WLAN and Mobile Security Plan

A security assessment and mitigation plan for a fictional company ("Alliah") covering wireless LAN and mobile device vulnerabilities.

### A. WLAN Vulnerabilities

| Vulnerability | Description |
|--------------|-------------|
| Weak/absent encryption | No specified WLAN encryption protocol; susceptible to unauthorized access if using outdated methods |
| Access point placement | AP placed outside on patio; exposed to **wardriving** attacks (attacker scans for vulnerable Wi-Fi networks while in motion) |

### B. Mobile Vulnerabilities

| Vulnerability | Description |
|--------------|-------------|
| Device loss/theft risk | Sales reps on the road 80% of the time carrying company-issued laptops, tablets, and smartphones — high exposure if lost or stolen |
| BYOD security gap | Personal devices brought into the company environment may have weaker security configurations than company-owned devices |

### C. Mitigation Steps

| Vulnerability | Mitigation |
|--------------|-----------|
| Weak WLAN encryption | Implement **WPA3** (AES encryption + strong password authentication) |
| AP placement | Conduct a **site survey** to optimize placement and minimize signal bleed beyond the perimeter |
| Device loss/theft | Deploy **Mobile Device Management (MDM)** software with remote data wipe capability |
| BYOD security | Install anti-malware/antivirus on all devices; conduct employee cybersecurity awareness training |

### D. Preventative Measures

- **WLAN:** Regular security audits; timely security patch updates; **network segmentation** to isolate critical systems from general-use networks
- **Compliance framework:** Follow **PCI DSS** (Payment Card Industry Data Security Standard) for security monitoring
- **Mobile/BYOD:** Employee training on phishing awareness and strong password hygiene per **FTC Cybersecurity for Small Businesses** guidelines
- **MDM compliance:** Adhere to **SOX (Sarbanes-Oxley Act)** to identify, protect, and safeguard financial data on mobile devices

### E. BYOD Approach

**Recommended solution: SASE (Secure Access Service Edge)**

- Combines network security services (secure web gateway, firewall-as-a-service, zero trust network access) with SD-WAN capabilities
- Cloud-delivered — accessible securely from any location, ideal for a highly mobile workforce
- Cost-effective alternative to on-premise security infrastructure
- Extends security controls to personal devices, remote users, and distributed locations

---

## Tools & Technologies Referenced

| Tool / Technology | Purpose |
|------------------|---------|
| **Nmap** | Network scanning; open port discovery; OS detection |
| **Wireshark** | Packet capture and protocol analysis |
| **WPA3** | WLAN encryption standard (AES + SAE authentication) |
| **MDM** | Mobile device management; remote wipe, policy enforcement |
| **SASE** | Cloud-based network security for BYOD and remote workers |
| **HTTPS / Port 443** | Encrypted web communication (replaces HTTP port 80) |
| **SFTP / Port 22** | Secure file transfer (replaces FTP port 21) |
| **IDPS** | Intrusion Detection and Prevention Systems |
| **TCP SACK** | Selective acknowledgement for TCP retransmission tuning |

---

## Standards & Compliance

| Standard | Relevance |
|---------|-----------|
| **PCI DSS** | Security monitoring and breach prevention for payment-related systems |
| **SOX (Sarbanes-Oxley Act)** | Financial data protection on mobile and MDM-managed devices |
| **FTC Cybersecurity for Small Businesses** | Employee training framework for BYOD and mobile threats |

---

## Sources

- Doherty, J. (2022). *Wireless and mobile device security*. Jones & Bartlett Learning.
- Cisco. (2023, July 24). *What is SASE – Secure Access Service Edge?* https://www.cisco.com/c/en/us/products/security/what-is-sase-secure-access-service-edge.html
- IBM. (n.d.). *What is SOX (Sarbanes-Oxley Act) compliance?* https://www.ibm.com/topics/sox-compliance
- Federal Trade Commission. (2021, December 17). *Cybersecurity for Small Business.* https://www.ftc.gov/business-guidance/small-businesses/cybersecurity
- Raath, S. (2023). *HTTPS port 443: What is it, and is it safe to open?* ExpressVPN. https://www.expressvpn.com/blog/https-port-443-what-is-it/
- Gillis, A. S. (2022). *Secure File Transfer Protocol (SFTP).* TechTarget. https://www.techtarget.com/searchcontentmanagement/definition/Secure-File-Transfer-Protocol-SSH-File-Transfer-Protocol
- U.S. Department of Defense. (n.d.). *Hardening network devices.* https://media.defense.gov/2020/Aug/18/2002479461/-1/-1/0/HARDENING_NETWORK_DEVICES.PDF
- CVE. (n.d.). *Search CVE list.* https://cve.mitre.org/cve/search_cve_list.html

---

*All work is original and based on WGU C844 Emerging Technologies in Cybersecurity course materials and lab environments.*
