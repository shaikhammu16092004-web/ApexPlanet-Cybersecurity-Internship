# 🛡️ Task 1 — Foundations of Cybersecurity
## ApexPlanet Software Pvt. Ltd. Internship

**Intern:** Amir Mustak Shaikh  
**Duration:** Days 1–12  
**Lab OS:** Kali Linux (VM)  
**Target:** DVWA (Damn Vulnerable Web Application)

---

## 📌 Objective
Build strong fundamentals in cybersecurity, networking, cryptography, and set up a professional ethical hacking lab environment.

---

## 🖥️ Lab Environment Setup

### Tools Installed
| Tool | Purpose |
|------|---------|
| VirtualBox | Virtualization platform |
| Kali Linux | Attacker machine |
| DVWA | Vulnerable web app target |
| Apache2 + MariaDB | Web + Database server |
| Wireshark | Packet capture & analysis |
| Nmap | Network scanning |
| Burp Suite | Web proxy & vulnerability scanner |
| OpenSSL | Cryptography hands-on |

### Setup Steps
```bash
# DVWA Installation
sudo apt update && sudo apt install apache2 php php-mysqli mariadb-server -y
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
sudo cp /var/www/html/DVWA/config/config.inc.php.dist /var/www/html/DVWA/config/config.inc.php
sudo chmod 777 /var/www/html/DVWA/hackable/uploads/
sudo chmod 777 /var/www/html/DVWA/config/
sudo service apache2 start && sudo service mariadb start

# Database Setup
sudo mysql
CREATE DATABASE dvwa;
CREATE USER 'dvwa'@'127.0.0.1' IDENTIFIED BY 'p@ssw0rd';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'127.0.0.1';
FLUSH PRIVILEGES;
EXIT;
```

**DVWA Access:** `http://127.0.0.1/DVWA` | admin / password

---

## 🔐 Cybersecurity Basics

### CIA Triad
| Principle | Definition | Example |
|-----------|-----------|---------|
| **Confidentiality** | Only authorized users can access data | Encryption, Passwords |
| **Integrity** | Data remains accurate and untampered | Hashing, Checksums |
| **Availability** | System accessible when needed | DDoS protection, Backups |

### Threat Types
| Threat | Description |
|--------|-------------|
| **Phishing** | Fake emails/sites to steal credentials |
| **Malware** | Ransomware, Trojans, Spyware |
| **DDoS** | Flood attack to make services unavailable |
| **SQL Injection** | Malicious SQL to manipulate databases |
| **Brute Force** | Automated password guessing |
| **Ransomware** | Encrypts files and demands payment |

### Attack Vectors
- **Social Engineering** — Manipulating humans to reveal information
- **Wireless Attacks** — WPA2 cracking, Evil Twin AP
- **Insider Threats** — Malicious or negligent employees

---

## 🌐 Networking Basics

### OSI Model
| Layer | Name | Protocol Examples |
|-------|------|------------------|
| 7 | Application | HTTP, DNS, SMTP |
| 6 | Presentation | SSL/TLS, Encryption |
| 5 | Session | NetBIOS, RPC |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP, ICMP, Routing |
| 2 | Data Link | Ethernet, MAC |
| 1 | Physical | Cables, Hardware |

> 🧠 Mnemonic: **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

### TCP/IP Suite
- **TCP** — Connection-oriented, reliable (3-way handshake: SYN → SYN-ACK → ACK)
- **UDP** — Connectionless, fast (DNS, VoIP, streaming)

### Key Ports
| Port | Protocol | Service |
|------|---------|---------|
| 22 | TCP | SSH |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| 53 | UDP | DNS |
| 3306 | TCP | MySQL/MariaDB |
| 3389 | TCP | RDP |

### Nmap Scan Results
```
PORT     STATE  SERVICE  VERSION
80/tcp   open   http     Apache httpd 2.4.68 ((Debian))
3306/tcp open   mysql    MariaDB 11.8.8
```
Command used: `nmap -sV 127.0.0.1`

---

## 🔒 Cryptography Basics

### Symmetric vs Asymmetric
| Type | Key | Speed | Example |
|------|-----|-------|---------|
| Symmetric | Same key encrypt/decrypt | Fast | AES-256 |
| Asymmetric | Public/Private key pair | Slower | RSA |

### Hashing
| Algorithm | Output Size | Status |
|-----------|------------|--------|
| MD5 | 128-bit | ⚠️ Weak (deprecated) |
| SHA-1 | 160-bit | ⚠️ Weak (deprecated) |
| SHA-256 | 256-bit | ✅ Secure |

### Hands-on: OpenSSL Demonstration

**Encrypt a message:**
```bash
echo "Amir Shaikh - ApexPlanet Internship" | openssl enc -aes-256-cbc -base64 -k "mypassword" -pbkdf2 > encrypted.txt
```
**Output:** `U2FsdGVkX181G6LdJu+WSrDC8O4sZ3yn5A181wdRTVsU35ibMfWW/NsE1WpNlGC4 1dUewlXO8ZzSPLfRYGX6Zg==`

**Decrypt the message:**
```bash
openssl enc -aes-256-cbc -d -base64 -k "mypassword" -pbkdf2 -in encrypted.txt
```
**Output:** `Amir Shaikh - ApexPlanet Internship` ✅

**SHA256 Hash:**
```bash
echo "Amir Shaikh" | sha256sum
# Output: 6aa8298356729d8f3ebafeb643b58b4ae71b4dc811f1b2c15a0777b9bb9d75cc
```

**MD5 Hash:**
```bash
echo "Amir Shaikh" | md5sum
# Output: 78ac0f095733af4b0befed9392906f47
```

---

## 🛠️ Tool Familiarization

### 1. Wireshark
- Captured live network packets on eth0 interface
- Observed TCP handshakes, TLS 1.2 encrypted traffic
- Identified source/destination IPs and protocols

### 2. Nmap
```bash
nmap -sV 127.0.0.1    # Service version detection
nmap -sC 127.0.0.1    # Default script scan
nmap -p- 127.0.0.1    # All ports scan
```

### 3. Burp Suite
- Community Edition v2026.7.2 configured
- Live passive crawl from proxy enabled
- Used for web traffic interception and analysis

### 4. Netcat
```bash
nc -lvnp 4444          # Listen on port 4444
nc 127.0.0.1 4444      # Connect to listener
```

---

## 📸 Screenshots
All screenshots available in `/screenshots/` folder:
1. `kali-desktop.png` — Kali Linux lab environment
2. `dvwa-dashboard.png` — DVWA running at localhost
3. `wireshark-capture.png` — Live packet capture (82 packets)
4. `nmap-scan.png` — Service version detection results
5. `openssl-demo.png` — Encrypt/Decrypt/Hash demonstration
6. `burpsuite.png` — Burp Suite Community Edition
7. `ifconfig.png` — Network interface configuration

---

## ✅ Task Completion Summary
- [x] Lab Environment Setup (Kali + DVWA)
- [x] Cybersecurity Basics (CIA Triad, Threats, Attack Vectors)
- [x] Linux Fundamentals (Commands practiced)
- [x] Networking Basics (OSI, TCP/IP, Ports)
- [x] Cryptography (OpenSSL AES-256 + SHA256 + MD5)
- [x] Tool Familiarization (Wireshark, Nmap, Burp Suite)

---

*ApexPlanet Software Pvt. Ltd. Cybersecurity Internship — Task 1*
