Task 4 — Exploitation & System Security
ApexPlanet Software Pvt. Ltd. Internship
Intern: Amir Mustak Shaikh
Duration: Days 37–48
Lab OS: Kali Linux (VM)
Target: Localhost (Apache/DVWA), Self (SSH)
Objective: Learn the penetration testing workflow and exploit vulnerabilities responsibly, then harden the system against similar attacks.

1️⃣ Penetration Testing Methodology
Phases Followed
Recon → Scanning → Exploitation → Post-Exploitation → Reporting

Recon & Scanning — Metasploit
Used Metasploit auxiliary scanner modules to fingerprint the target before any exploitation attempt.

msf6 > use auxiliary/scanner/http/http_version
msf6 > set RHOSTS 127.0.0.1
msf6 > set RPORT 80
msf6 > run

Result: 127.0.0.1:80 Apache/2.4.68 (Debian) ✅

msf6 > use auxiliary/scanner/http/dir_scanner
msf6 > run

Result: Found /icons/ and /javascript/ (403 Forbidden) ✅

msf6 > use auxiliary/scanner/http/robots_txt
msf6 > run

Result: No robots.txt found — valid recon finding

2️⃣ Password Attacks
SSH Brute-Force — Hydra
Target: Local SSH service (self-hosted, port 22)

hydra -l shaikh -P passwords.txt ssh://127.0.0.1

Result: Valid password found ✅
[22][ssh] host: 127.0.0.1   login: shaikh   password: ********
1 of 1 target successfully completed, 1 valid password found

Hash Cracking — John the Ripper
Step 1 — Generate an MD5 hash:

echo -n "password123" | md5sum
→ 482c811da5d5b4bc6d497ffa98491e38

Step 2 — Crack it:

echo "482c811da5d5b4bc6d497ffa98491e38" > hash.txt
john --format=raw-md5 --wordlist=mywordlist.txt hash.txt
john --show --format=Raw-MD5 hash.txt

Result: ?:password123 — 1 password hash cracked ✅

3️⃣ Social Engineering (Simulation Only)
Phishing Simulation Page
Built a local fake login page mimicking a generic "Secure Account Portal," clearly labeled as a simulation with no real data capture.

mkdir -p ~/Task4/phishing-simulation
python3 -m http.server 8080
→ http://localhost:8080

Result: Login form rendered and submission flow tested (POST captured in server logs) ✅

Awareness Training Content
Documented phishing red flags for awareness training, covering:

Suspicious/lookalike URLs
Missing HTTPS / invalid certificates
Urgency & pressure tactics
Generic greetings, poor grammar
Unexpected attachments/links
Requests for sensitive info via email/forms
Full write-up: notes/phishing-awareness.md

4️⃣ Malware Basics
Static Analysis
Used the industry-standard EICAR test file (safe, non-malicious) to demonstrate malware analysis fundamentals.

file eicar_test.txt        → EICAR virus test files
md5sum eicar_test.txt      → 69630e4574ec6798239b091cda43dca0
sha256sum eicar_test.txt   → 131f95c51cc819465fa1797f6ccacf9d494aaaff46fa3eac73ae63ffbdfd8267

Dynamic Analysis — Sandbox Scan (ClamAV)
sudo apt install clamav -y
sudo freshclam
clamscan eicar_test.txt

Result: eicar_test.txt: Eicar-Signature FOUND — Infected files: 1 ✅
Confirms signature-based detection engine correctly flagged the test sample.

5️⃣ System Hardening
Security Patches
sudo apt update && sudo apt upgrade -y

Firewall Configuration — UFW
sudo apt install ufw -y
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw status verbose

Result:
Status: active
Default: deny (incoming), allow (outgoing)
22/tcp ALLOW IN Anywhere ✅

Disabling Unused Services
Reviewed all running services and disabled unnecessary ones to reduce attack surface:

sudo systemctl disable --now pcscd.service
sudo systemctl disable --now ModemManager.service
sudo systemctl disable --now colord.service

Result: Running services reduced from 22 → 19 ✅ (pcscd, ModemManager, colord removed — smart card, mobile broadband, and color management daemons not needed on this VM)

📊 Task Coverage Summary
Step	Activity	Status
1	Penetration Testing Methodology (Recon → Reporting)	✅ Documented
2	Exploitation with Metasploit (http_version, dir_scanner, robots_txt)	✅ Completed
3	Password Attacks (Hydra SSH brute-force + John the Ripper hash cracking)	✅ Completed
4	Social Engineering (Phishing simulation + awareness training)	✅ Completed
5	Malware Basics (Static + Dynamic/sandbox analysis)	✅ Completed
6	System Hardening (Patches + Firewall + Service reduction)	✅ Completed
📸 Screenshots
All screenshots in /screenshots/ folder:

File	Description
metasploit.png	Metasploit http_version scan — Apache version identified
metasploit1.png	Metasploit dir_scanner — directories discovered
msfconsole1.png	Metasploit robots_txt scanner run
hydra-bruteforce-final.png	Hydra SSH brute-force — valid password found
john_the_ripper.png	MD5 hash generation
malware_analysis.png	John the Ripper wordlist crack result
malware_analysis1.png	John the Ripper run in progress
phishing.png	Phishing simulation page — browser view
phishing_setup.png	Phishing simulation — local server setup
phishing_page.png	Phishing page — server logs (POST captured)
firewall.png	UFW firewall — active status and rules
✅ Task 4 Completion Summary
 Penetration Testing Methodology — 5 phases documented with real examples
 Metasploit Exploitation — 3 recon/scanner modules run against local Apache server
 Password Attacks — SSH brute-forced with Hydra, MD5 hash cracked with John the Ripper
 Social Engineering — phishing simulation page built and tested + awareness training notes
 Malware Basics — EICAR test file analyzed via static methods and ClamAV dynamic scan
 System Hardening — system patched, firewall configured (default-deny), 3 unused services disabled

ApexPlanet Software Pvt. Ltd. Cybersecurity Internship — Task 4
