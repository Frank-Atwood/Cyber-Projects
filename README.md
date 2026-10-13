# Cyber-Projects

**Frank "Trey" Atwood** · Cybersecurity graduate, Appalachian State University (BS, May 2026) · Charlotte, NC

Hands-on security labs I build and document on my own time: cloud security and GRC, SIEM and IDS engineering, and offensive/defensive practice. Every project includes objectives, tools, methodology, screenshots, and key takeaways.

🔎 **Open to:** SOC Analyst · GRC / Risk Analyst · Digital Forensics roles in the Charlotte area
📫 **Connect:** [LinkedIn]([https://www.linkedin.com/in/frankatwood/) · [Email](treyatwoodpro@gmail.com)


![Security+](https://img.shields.io/badge/CompTIA-Security%2B%20(SY0--701)-C8202F?style=flat-square)
![AWS CCP](https://img.shields.io/badge/AWS-Cloud%20Practitioner-FF9900?style=flat-square&logo=amazonaws&logoColor=white)
![Google](https://img.shields.io/badge/Google-Cybersecurity%20Certificate-4285F4?style=flat-square&logo=google&logoColor=white)

---

## ⭐ Featured Project

### [AWS Cloud Security Risk Assessment & GRC Lab](https://github.com/Frank-Atwood/aws-grc-lab)
Built a deliberately misconfigured AWS environment for a fictional healthcare practice, then ran it through a full risk-management lifecycle.

- **Assessed** with AWS Security Hub CSPM against NIST 800-53, CIS, and AWS FSBP; baseline compliance score of **30%**
- **Identified 10 risks**: public S3 bucket holding (fake) patient data, SSH/RDP open to the internet, over-privileged IAM user with static keys and no MFA, no CloudTrail logging, and more
- **Remediated 7, formally accepted 3**, verified every fix at the resource level, and cut Critical/High findings from 15 to 9 *(final score: pending re-evaluation)*
- **Delivered** a risk register, remediation record, executive summary, and POA&M

`AWS` `Security Hub` `IAM` `S3` `CloudTrail` `NIST 800-53` `CIS Benchmarks` `Risk Register` `POA&M`

---

## 🖥️ Home Lab

A Proxmox VE server (Dell OptiPlex 7050) running an isolated security lab, reachable over OpenVPN.

| Area | What I run |
|---|---|
| **SIEM & Detection** | Wazuh SIEM with agents on lab hosts; Suricata IDS with custom rules for SQLi, XSS, and command injection forwarding alerts into Wazuh |
| **Log Analysis** | Splunk on Ubuntu Server with Boss of the SOC (BOTS) datasets for SPL practice |
| **Attack / Defend** | Kali Linux vs. Metasploitable and DVWA targets |
| **Monitoring** | Grafana + InfluxDB metrics pipeline, Uptime Kuma |
| **Network Services** | Pi-hole DNS filtering, Nginx Proxy Manager, Homarr dashboard |

---

## 📂 Repository Contents

| Folder | Description |
|---|---|
| `Ethical Hacking (Course) PPTs` | Presentations I built for my Ethical Hacking course, covering topics from exploitation through prevention |
| *More coming* | New lab write-ups are added as I complete them |

---

## 🎓 Education & Experience

**BS in Cybersecurity, Appalachian State University** (May 2026)
Relevant coursework: Audit & Cybersecurity Analytics, Managing Securities, Network & IT Infrastructures, Database Management, Global IS Ethics & Privacy, Programming Software Solutions

- Competed in the **Microsoft Security Immersion Challenge** hosted at App State ([Credly](YOUR-CREDLY-LINK))
- Forensics tooling from coursework: Autopsy, Volatility, Wireshark / PCAP analysis
- Platforms: Hack The Box Starting Point

---

## 🛠️ Skills & Tools

**Cloud & GRC:** AWS (IAM, S3, EC2, CloudTrail, Security Hub, Config), NIST 800-53, CIS Benchmarks, risk registers, POA&M
**Detection & Response:** Wazuh, Splunk (SPL), Suricata, Wireshark
**Forensics:** Autopsy, Volatility
**Offensive:** Kali Linux, Metasploit, DVWA
**Infrastructure:** Proxmox VE, Linux, Docker/LXC, OpenVPN, DNS

---

## 📜 Certifications

| Certification | Status |
|---|---|
| CompTIA Security+ (SY0-701) | ✅ Earned |
| AWS Certified Cloud Practitioner | ✅ Earned (Sept 2026) |
| Google Cybersecurity Professional Certificate | ✅ Earned ([Credly](YOUR-CREDLY-LINK)) |
| Splunk Core Certified User | 🎯 Next up |
