# 🌐 Task 2 — Network Security & Scanning
## ApexPlanet Software Pvt. Ltd. Internship

**Intern:** Amir Mustak Shaikh  
**Duration:** Days 13–24  
**Lab OS:** Kali Linux (VM)  
**Target:** localhost (127.0.0.1)

---

## 📌 Objective
Learn reconnaissance, scanning, and network traffic analysis using industry-standard tools.

---

## 1️⃣ Reconnaissance

### Passive Reconnaissance

#### WHOIS Lookup
```bash
whois google.com
```
**Findings:**
| Field | Value |
|-------|-------|
| Domain | google.com |
| Registrar | MarkMonitor Inc. |
| Created | 1997-09-15 |
| Expires | 2028-09-14 |
| Organization | Google LLC |
| Country | US |
| Name Servers | ns1–ns4.google.com |
| DNSSEC | Unsigned |

#### Nslookup
```bash
nslookup google.com
```
**Findings:**
- DNS Server: 192.168.0.1 (Port 53)
- IPv4: 142.250.70.78
- IPv6: 2404:6800:4009:809::200e

### Active Reconnaissance

#### Ping Sweep
```bash
ping -c 4 google.com
```
**Findings:**
- Target IP: 142.251.43.14
- Packets: 4 sent, 4 received, **0% packet loss**
- RTT avg: 26.599ms — Host is alive!

#### Banner Grabbing
```bash
nc -v google.com 80
```
**Findings:**
- google.com [142.250.70.78] Port 80 — OPEN
- HTTP service confirmed running

#### theHarvester
```bash
theHarvester -d google.com -l 50 -b bing
```
- Tool: theHarvester v4.11.1
- Purpose: Email & subdomain enumeration
- Used for passive OSINT reconnaissance

---

## 2️⃣ Port & Service Scanning

### TCP SYN Scan (-sS)
```bash
nmap -sS 127.0.0.1
```
**Results:**
| Port | State | Service |
|------|-------|---------|
| 80/tcp | open | http |

### Service Version Detection (-sV)
```bash
nmap -sV 127.0.0.1
```
**Results:**
| Port | Service | Version |
|------|---------|---------|
| 80/tcp | http | Apache httpd 2.4.68 (Debian) |

### OS Detection (-O)
```bash
sudo nmap -O 127.0.0.1
```
**Results:**
- OS: Linux (Kali — Debian-based)
- TCP/IP fingerprint generated
- Network Distance: 0 hops (localhost)

### Full Aggressive Scan (-A)
```bash
sudo nmap -A 127.0.0.1
```
**Results:**
- Apache httpd 2.4.68 confirmed
- HTTP Title: "Apache2 Debian Default Page"
- OS fingerprint: x86_64 Linux

---

## 3️⃣ Vulnerability Scanning

### Nmap Vulnerability Scripts
```bash
sudo nmap --script vuln 127.0.0.1
```
**Results:**
| Port | Findings |
|------|---------|
| 80/tcp | `/server-status/` — Potentially interesting folder |
| 80/tcp | No CSRF vulnerabilities found |
| 80/tcp | No DOM-based XSS found |
| 80/tcp | No Stored XSS found |
| 5432/tcp | PostgreSQL detected |

**Analysis:**
- `/server-status/` exposed — Information disclosure risk (Medium)
- No critical vulnerabilities found in lab environment
- PostgreSQL running on port 5432

---

## 4️⃣ Packet Analysis with Wireshark

### Traffic Generation
```bash
# HTTP traffic
curl http://127.0.0.1/DVWA

# DNS traffic  
nslookup google.com

# FTP test
ftp 127.0.0.1
```

**Results:**
- HTTP: Apache 301 redirect detected
- DNS: google.com → 142.251.43.14 resolved
- FTP: Port 21 closed (service not running)

### Wireshark Capture
- Interface: eth0
- Packets captured: **2847**
- Protocols observed: TCP, TLS v1.2/1.3, DNS (UDP Port 53)
- DNS Query detected: Domain Name System query visible
- TLS Application Data: Encrypted HTTPS traffic captured

### SYN Flood Simulation (hping3)
```bash
sudo hping3 -S --flood -V -p 80 127.0.0.1
```
**Results:**
- **17,826,900 packets transmitted** in seconds
- Interface: lo (loopback), MTU: 65536
- 100% packet loss (flood mode — no replies shown)
- **DDoS simulation successfully demonstrated!**

---

## 5️⃣ Firewall Basics (iptables)

### Rules Created
```bash
# View rules
sudo iptables -L -v

# Allow HTTP (Port 80)
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Block Telnet (Port 23)
sudo iptables -A INPUT -p tcp --dport 23 -j DROP

# Block NULL packet scans
sudo iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP
```

### Firewall Rules Applied
| Rule | Port | Protocol | Action |
|------|------|---------|--------|
| Allow HTTP | 80 | TCP | ACCEPT |
| Block Telnet | 23 | TCP | DROP |
| Block NULL scan | ALL | TCP | DROP |

### Block Demonstration
```bash
# Test blocked Telnet
nc -v 127.0.0.1 23
# Result: Connection refused ✅ — BLOCKED!

# Nmap scan with firewall active
sudo nmap -sS 127.0.0.1
# Result: Port 23 not shown — successfully blocked!
```

### Clear Rules
```bash
sudo iptables -F
```

---

## 📊 Scan Report Summary

| Target | IP | Open Ports | Services | Vulnerabilities |
|--------|-----|-----------|---------|----------------|
| localhost | 127.0.0.1 | 80, 5432 | Apache 2.4.68, PostgreSQL | /server-status/ exposed (Medium) |
| google.com | 142.250.70.78 | 80 | HTTP | N/A (external, not tested) |

### Risk Rating
| Finding | Severity | Recommendation |
|---------|---------|---------------|
| /server-status/ exposed | Medium | Disable mod_status in Apache config |
| Port 5432 PostgreSQL open | Low | Bind to localhost only |
| Apache version disclosed | Low | Use ServerTokens Prod in httpd.conf |

---

## 📸 Screenshots
All screenshots in `/screenshots/` folder:
1. `ping.jpeg` — Ping sweep & banner grabbing
2. `Harvester.jpeg` — theHarvester OSINT tool
3. `detections.jpeg` — Nmap service/OS detection scans
4. `nmapscaan.jpeg` — Nmap vulnerability scripts
5. `vulnerabality_scanning.jpeg` — OpenVAS/GVM install
6. `traffic_genrate.jpeg` — HTTP/DNS/FTP traffic generation
7. `SYN_flood.jpeg` — hping3 SYN flood simulation
8. `task2_wiresherk.jpeg` — Wireshark packet capture (2847 packets)
9. `iptables.jpeg` — Firewall rules configuration

---

## ✅ Task 2 Completion Summary
- [x] Passive Recon — WHOIS, Nslookup, theHarvester
- [x] Active Recon — Ping sweep, Banner grabbing
- [x] Port Scanning — TCP SYN, Service version, OS detection, Aggressive scan
- [x] Vulnerability Scanning — Nmap vuln scripts
- [x] Packet Analysis — Wireshark (2847 packets), HTTP/DNS/TLS traffic
- [x] SYN Flood Simulation — hping3 (17.8M packets)
- [x] Firewall Rules — iptables allow/deny, block demonstration

---

*ApexPlanet Software Pvt. Ltd. Cybersecurity Internship — Task 2*
