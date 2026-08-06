# 🛡️ ApexPlanet Cybersecurity Internship

[![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux-557C94?logo=linux&logoColor=white)](https://www.kali.org/)
[![CEH](https://img.shields.io/badge/Cert-CEH%20Certified-red?logo=ec-council)](https://www.eccouncil.org/)
[![DVWA](https://img.shields.io/badge/Target-DVWA-orange)](https://github.com/digininja/DVWA)
[![GitHub](https://img.shields.io/badge/Status-Active-brightgreen)]()
[![Internship](https://img.shields.io/badge/Company-ApexPlanet%20Software-blue)](https://www.apexplanet.in)

> **Intern:** Amir Mustak Shaikh  
> **Company:** ApexPlanet Software Pvt. Ltd.  
> **Domain:** Cybersecurity & Ethical Hacking  
> **LinkedIn:** [linkedin.com/in/amir-shaikh-a3720531b](https://linkedin.com/in/amir-shaikh-a3720531b)

---

## 📌 About This Repository

This repository contains all hands-on tasks completed during the **ApexPlanet Software Pvt. Ltd. Cybersecurity Internship**. Each task covers a critical domain of cybersecurity — from foundational concepts and lab setup to advanced penetration testing, exploitation, and incident response.

All tasks are performed in a **legal, isolated lab environment** using Kali Linux, DVWA, and industry-standard security tools.

---

## 🗂️ Task Overview

| Task | Topic | Status | Duration |
|------|-------|--------|----------|
| [Task 1](./Task-1/README.md) | Foundations of Cybersecurity & Lab Setup | ✅ Complete | Days 1–12 |
| Task 2 | Network Security & Scanning | 🔄 In Progress | Days 13–24 |
| Task 3 | Web Application Security | ⏳ Upcoming | Days 25–36 |
| Task 4 | Exploitation & System Security | ⏳ Upcoming | Days 37–48 |
| Task 5 | Capstone Project & Incident Response | ⏳ Upcoming | Days 49–60 |

---

## 🧰 Tools & Technologies

| Category | Tools |
|----------|-------|
| **Attacker OS** | Kali Linux |
| **Target App** | DVWA (Damn Vulnerable Web Application) |
| **Network Scanning** | Nmap, Masscan |
| **Packet Analysis** | Wireshark |
| **Web Proxy** | Burp Suite Community Edition |
| **Exploitation** | Metasploit Framework |
| **Cryptography** | OpenSSL |
| **SIEM** | Splunk Enterprise |
| **Threat Detection** | MITRE ATT&CK, Atomic Red Team |
| **Scripting** | Python, Bash |

---

## 📁 Repository Structure

```
ApexPlanet-Cybersecurity-Internship/
│
├── Task-1/
│   ├── README.md                          ← Lab Setup Report
│   ├── linux-cheatsheet.md                ← Linux Commands Reference
│   ├── networking-cryptography-notes.md   ← Networking & Crypto Notes
│   └── screenshots/                       ← Lab Evidence Screenshots
│       ├── kali-desktop.jpeg
│       ├── dvwa.jpeg
│       ├── nmap.jpeg
│       ├── wireshark.jpeg
│       ├── emcryption.jpeg
│       ├── burp suite.jpeg
│       ├── terminal.jpeg
│       └── main desktop 1.jpeg
│
├── Task-2/                                ← Coming Soon
├── Task-3/                                ← Coming Soon
├── Task-4/                                ← Coming Soon
├── Task-5/                                ← Coming Soon
│
└── README.md                              ← This file
```

---

## 🔐 Task 1 Highlights — Foundations of Cybersecurity

### ✅ Lab Environment
- Kali Linux VM (Attacker Machine)
- DVWA deployed on Apache2 + MariaDB
- Private lab network configured

### ✅ Key Concepts Covered
- CIA Triad (Confidentiality, Integrity, Availability)
- Threat Types: Phishing, Malware, DDoS, SQL Injection, Ransomware
- OSI Model & TCP/IP Protocol Suite
- Symmetric vs Asymmetric Encryption
- Hashing: MD5, SHA256

### ✅ Hands-on Demonstrations
```bash
# Network Scanning
nmap -sV 127.0.0.1
# Result: Port 80 (Apache), Port 3306 (MariaDB)

# AES-256 Encryption
echo "Amir Shaikh - ApexPlanet Internship" | openssl enc -aes-256-cbc -base64 -k "mypassword" -pbkdf2

# SHA256 Hashing
echo "Amir Shaikh" | sha256sum
# 6aa8298356729d8f3ebafeb643b58b4ae71b4dc811f1b2c15a0777b9bb9d75cc
```

---

## 🚀 About ApexPlanet Software Pvt. Ltd.

[ApexPlanet Software Pvt. Ltd.](https://www.apexplanet.in) delivers secure, high-performance web and mobile applications, blending cutting-edge technology with cybersecurity best practices. The internship program trains the next generation of security professionals through hands-on, real-world tasks.

---

## 📜 Disclaimer

> All security testing and exploitation techniques demonstrated in this repository are performed **strictly in a controlled, isolated lab environment** for educational purposes only. No real systems were targeted. Unauthorized penetration testing is illegal.

---

## 📬 Connect

- 🔗 **LinkedIn:** [Amir Shaikh](https://linkedin.com/in/amir-shaikh-a3720531b)
- 💻 **GitHub:** [shaikhammu16092004-web](https://github.com/shaikhammu16092004-web)
- 📧 **Email:** shaikhammu16092004@gmail.com

---

*© 2026 Amir Mustak Shaikh | ApexPlanet Software Pvt. Ltd. Cybersecurity Internship*
