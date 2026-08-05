# 🌐 Networking & Cryptography Notes
## ApexPlanet Cybersecurity Internship — Task 1

---

## OSI Model — 7 Layers

| Layer | Name | Function | Protocols | Attack Examples |
|-------|------|----------|-----------|----------------|
| 7 | Application | User interface | HTTP, DNS, SMTP, FTP | XSS, SQLi, Phishing |
| 6 | Presentation | Encryption, Format | SSL/TLS, JPEG | SSL Stripping |
| 5 | Session | Session management | NetBIOS, RPC | Session Hijacking |
| 4 | Transport | End-to-end delivery | TCP, UDP | SYN Flood, Port Scan |
| 3 | Network | Routing, IP | IP, ICMP, OSPF | IP Spoofing, MITM |
| 2 | Data Link | MAC addressing | Ethernet, ARP | ARP Spoofing |
| 1 | Physical | Physical signals | Cables, Wi-Fi | Cable tapping |

> 🧠 **Mnemonic:** **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

---

## TCP/IP Protocol Suite

### TCP vs UDP
| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery | Best effort |
| Speed | Slower | Faster |
| Use Case | HTTP, SSH, FTP | DNS, VoIP, Gaming |
| Handshake | 3-way (SYN/SYN-ACK/ACK) | None |

### TCP 3-Way Handshake
```
Client          Server
  |---SYN------->|   "I want to connect"
  |<--SYN-ACK----|   "OK, ready"
  |---ACK------->|   "Connected!"
```

---

## DNS & HTTP/HTTPS Deep Dive

### DNS Resolution Process
```
Browser → Local Cache → /etc/hosts → DNS Resolver → Root DNS → TLD DNS → Authoritative DNS
```

### HTTP vs HTTPS
| Feature | HTTP (Port 80) | HTTPS (Port 443) |
|---------|---------------|-----------------|
| Encryption | None (plain text) | SSL/TLS encrypted |
| Security | ❌ Vulnerable to MITM | ✅ Secure |
| Certificate | Not required | SSL Certificate required |

### SSL/TLS Handshake
```
1. Client Hello (supported ciphers)
2. Server Hello + Certificate
3. Key Exchange
4. Session Keys Generated
5. Encrypted Communication Begins
```

---

## IP Addressing & Subnetting

### IPv4 Classes
| Class | Range | Default Subnet | Use |
|-------|-------|---------------|-----|
| A | 1.0.0.0 – 126.255.255.255 | /8 | Large networks |
| B | 128.0.0.0 – 191.255.255.255 | /16 | Medium networks |
| C | 192.0.0.0 – 223.255.255.255 | /24 | Small networks |

### Private IP Ranges
```
10.0.0.0/8        — Class A private
172.16.0.0/12     — Class B private
192.168.0.0/16    — Class C private
127.0.0.1         — Loopback (localhost)
```

### Common Subnet Masks
| CIDR | Subnet Mask | Hosts |
|------|------------|-------|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /30 | 255.255.255.252 | 2 |

---

## Common Ports Reference

| Port | Protocol | Service | Security Note |
|------|---------|---------|--------------|
| 21 | TCP | FTP | ⚠️ Unencrypted |
| 22 | TCP | SSH | ✅ Encrypted |
| 23 | TCP | Telnet | ❌ Never use |
| 25 | TCP | SMTP | Email |
| 53 | UDP/TCP | DNS | DNS tunneling risk |
| 80 | TCP | HTTP | ⚠️ Unencrypted |
| 443 | TCP | HTTPS | ✅ Encrypted |
| 3306 | TCP | MySQL | ⚠️ Don't expose |
| 3389 | TCP | RDP | ⚠️ Brute force target |
| 4444 | TCP | Metasploit default | 🔴 Red flag |

---

## Cryptography Basics

### Symmetric Encryption
- **Same key** for encryption and decryption
- Fast, used for bulk data
- Key distribution problem
- **Algorithms:** AES-128, AES-256, DES (deprecated), 3DES

### Asymmetric Encryption
- **Public key** = encrypt, **Private key** = decrypt
- Slower but solves key distribution
- Used in SSL/TLS, Email signing
- **Algorithms:** RSA, ECC, Diffie-Hellman

### Hashing
- **One-way function** — cannot reverse
- Same input = always same output
- Used for password storage, integrity checks
- **Algorithms:**

| Algorithm | Bits | Status |
|-----------|------|--------|
| MD5 | 128 | ❌ Broken (collision attacks) |
| SHA-1 | 160 | ❌ Deprecated |
| SHA-256 | 256 | ✅ Secure |
| SHA-3 | 256+ | ✅ Most secure |
| bcrypt | Variable | ✅ Best for passwords |

### Digital Certificates & SSL/TLS
```
Certificate contains:
- Domain name
- Public key
- Issuing CA (Certificate Authority)
- Validity period
- Digital signature
```

**Certificate Authorities (CA):** DigiCert, Let's Encrypt, Comodo

---

## Hands-on: OpenSSL Lab Results

### AES-256-CBC Encryption
```bash
Command:
echo "Amir Shaikh - ApexPlanet Internship" | openssl enc -aes-256-cbc -base64 -k "mypassword" -pbkdf2

Encrypted Output:
U2FsdGVkX181G6LdJu+WSrDC8O4sZ3yn5A181wdRTVsU35ibMfWW/NsE1WpNlGC4
1dUewlXO8ZzSPLfRYGX6Zg==
```

### Decryption Verification
```bash
Command:
openssl enc -aes-256-cbc -d -base64 -k "mypassword" -pbkdf2 -in encrypted.txt

Decrypted Output:
Amir Shaikh - ApexPlanet Internship ✅
```

### Hashing Results
```bash
SHA256: 6aa8298356729d8f3ebafeb643b58b4ae71b4dc811f1b2c15a0777b9bb9d75cc
MD5:    78ac0f095733af4b0befed9392906f47

Observation: Same input = same hash (deterministic)
Even 1 character change = completely different hash (avalanche effect)
```

---

## NAT (Network Address Translation)
- Translates private IPs to public IP
- Allows multiple devices to share one public IP
- Types: Static NAT, Dynamic NAT, PAT (Port Address Translation)
- Our lab: VirtualBox NAT — Kali VM IP: 10.0.2.15

---

*ApexPlanet Software Pvt. Ltd. Cybersecurity Internship — Task 1*
