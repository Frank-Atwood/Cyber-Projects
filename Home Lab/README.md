# Home Lab — Dell OptiPlex 7050

A personal cybersecurity home lab I built while finishing my bachelor's degree in cybersecurity at Appalachian State University. The goal was to get hands-on experience with tools and concepts I was learning in class — things like network monitoring, intrusion detection, and web application attacks.

Everything runs on a used Dell OptiPlex 7050 I repurposed as a home server using Proxmox, a free hypervisor that lets you run multiple virtual machines and containers on one physical machine.

---

## What I Built

The lab has three main areas:

**Infrastructure** — the foundation that keeps everything running and organized

**Monitoring** — tools that let me see what's happening across the lab in real time

**Security** — the core of the lab, where I run attacks and practice detecting them

---

## Services Running

### Infrastructure

| Service | What it does |
|---------|-------------|
| Pi-Hole | Blocks ads and malicious domains at the DNS level for my entire network. Currently blocking about 57% of all DNS queries |
| Nginx Proxy Manager | Routes web traffic to the right services on my network |
| Homarr | A dashboard that shows all my services and live system stats in one place |
| Uptime Kuma | Monitors whether each service is up or down and alerts me if something goes offline |

### Monitoring

| Service | What it does |
|---------|-------------|
| InfluxDB | Stores time-series data like CPU and RAM usage from all my containers |
| Grafana | Turns that data into visual graphs so I can see how my system is performing over time |

I set these up by connecting them with a tool called Telegraf, it collects the metrics and sends them to InfluxDB, which Grafana then reads and displays.

### Security

| Service | What it does |
|---------|-------------|
| Wazuh | A SIEM (Security Information and Event Management) tool. It collects logs from every machine in my lab and alerts me when something suspicious happens |
| Suricata | A network intrusion detection system. It sits on my network bridge and inspects every packet passing between my containers, looking for known attack patterns |
| DVWA | Damn Vulnerable Web App. an intentionally insecure website I use as a practice target for web attacks |
| Kali Linux | My attack machine. I use it to run attacks against DVWA and watch them get detected |

---

## Attack and Detection Labs

The most valuable part of this lab is being able to run real attacks and see exactly how they look from a defender's perspective.

### SQL Injection
SQL injection is when an attacker manipulates a database query by injecting their own SQL code into a web form. I ran several SQL injection payloads against DVWA and watched:
- Suricata flag the request as a **Priority 1 Web Application Attack**
- Wazuh generate a **Level 6 alert** tagged with MITRE ATT&CK technique **T1190 (Exploit Public-Facing Application)**

This showed me that the same attack gets detected differently at the network layer (Suricata) vs the host/log layer (Wazuh), and why having both matters.

### XSS (Cross-Site Scripting)
XSS attacks inject malicious scripts into a web page that run in another user's browser. I learned that XSS is primarily a client-side attack — it doesn't touch the server the same way SQL injection does, which means it shows up differently in logs. Suricata caught it at the network layer by spotting the script tag in the HTTP request.

### Command Injection
Command injection is when an attacker tricks a web app into running operating system commands. I tested payloads against DVWA's command injection page. This taught me about the difference between attacks sent in a URL (GET requests) vs attacks sent in a form submission (POST requests) — they require different detection approaches.

---

## What I Learned

- How to set up and manage a virtualization environment from scratch
- How a SIEM works and how to read and interpret security alerts
- How network intrusion detection works and how to write basic detection rules
- How common web attacks (SQL injection, XSS, command injection) actually work in practice
- Why defense-in-depth matters — different tools catch different things
- How the MITRE ATT&CK framework maps to real attacks
- How to build a metrics and observability pipeline

---

## What's Next

- **Metasploitable** — a vulnerable VM for practicing more advanced exploitation with Metasploit
- **REMnux** — a Linux distro built for malware analysis
- **Greenbone/OpenVAS** — vulnerability scanning to find weaknesses in my own lab
- **Zeek** — another network analysis tool to pair with Suricata

---

## Screenshots
 
| Screenshot | Description |
|------------|-------------|
| Homarr Dashboard | All services running with live CPU/RAM stats |
| Proxmox UI | All containers and VMs with uptime and resource usage |
| Wazuh Dashboard | MITRE ATT&CK detections and multi-agent alerts |
| Suricata fast.log | Real-time attack detection output |
| Network Map | Full architecture diagram |
