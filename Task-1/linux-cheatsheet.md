# 🐧 Linux Commands Cheat Sheet
## ApexPlanet Cybersecurity Internship — Task 1

---

## 📁 File System Navigation
```bash
pwd                    # Current directory dikhao
ls                     # Files list karo
ls -la                 # Hidden files bhi dikhao (permissions ke saath)
cd /path/to/dir        # Directory change karo
cd ..                  # Ek level upar jao
cd ~                   # Home directory pe jao
tree                   # Directory structure dikhao
```

---

## 📄 File & Directory Operations
```bash
touch file.txt         # Empty file banao
mkdir myfolder         # New directory banao
mkdir -p a/b/c         # Nested directories banao
cp file.txt backup.txt # File copy karo
mv file.txt new.txt    # File move/rename karo
rm file.txt            # File delete karo
rm -rf folder/         # Folder forcefully delete karo (careful!)
cat file.txt           # File content dikhao
nano file.txt          # File edit karo (nano editor)
less file.txt          # File page by page dikhao
head -10 file.txt      # Pehli 10 lines dikhao
tail -f /var/log/syslog # Real-time log monitor karo
```

---

## 🔐 File & Directory Permissions
```bash
ls -l                  # Permissions dikhao
chmod 777 file         # rwxrwxrwx (sabko full access)
chmod 755 file         # rwxr-xr-x (owner full, others read/execute)
chmod 644 file         # rw-r--r-- (owner rw, others read only)
chmod +x script.sh     # Execute permission do
chown user:group file  # Owner change karo
chown -R www-data /var/www/html  # Recursive ownership change

# Permission Numbers
# 4 = Read (r)
# 2 = Write (w)  
# 1 = Execute (x)
# 7 = rwx | 6 = rw- | 5 = r-x | 4 = r--
```

---

## 📦 Package Management
```bash
sudo apt update              # Package list update karo
sudo apt upgrade             # Installed packages upgrade karo
sudo apt install nmap        # Package install karo
sudo apt remove nmap         # Package remove karo
sudo apt autoremove          # Unused packages hatao
sudo apt search wireshark    # Package search karo
dpkg -l                      # Installed packages list
dpkg -i package.deb          # .deb file install karo
```

---

## 🌐 Networking Commands
```bash
ifconfig                     # Network interfaces dikhao
ip addr show                 # IP addresses dikhao (modern)
ping google.com              # Connectivity test karo
ping -c 4 8.8.8.8           # 4 packets bhejo
netstat -an                  # All connections dikhao
netstat -tulnp               # Listening ports dikhao
ss -tuln                     # Socket statistics (modern netstat)
traceroute google.com        # Route trace karo
nslookup google.com          # DNS lookup karo
dig google.com               # Detailed DNS query
curl http://example.com      # HTTP request bhejo
wget http://example.com/file # File download karo
```

---

## 🔍 Search & Filter
```bash
grep "error" file.txt        # Pattern search karo
grep -r "password" /var/www/ # Recursive search
grep -i "ERROR" file.txt     # Case insensitive search
find / -name "*.txt"         # Files dhundho naam se
find / -type f -perm 777     # World-writable files dhundho
locate filename              # Fast file search
which nmap                   # Command location dhundho
```

---

## ⚙️ Process Management
```bash
ps aux                       # Running processes dikhao
ps aux | grep apache         # Specific process dhundho
top                          # Real-time process monitor
htop                         # Better process monitor
kill 1234                    # Process ID se kill karo
killall firefox              # Name se kill karo
jobs                         # Background jobs dikhao
bg                           # Background mein bhejo
fg                           # Foreground mein lao
```

---

## 🛡️ Security-Specific Commands
```bash
# Nmap scanning
nmap -sV 192.168.1.1         # Version detection
nmap -sC 192.168.1.1         # Default scripts
nmap -p 1-1000 192.168.1.1   # Port range scan
nmap -O 192.168.1.1          # OS detection
nmap -A 192.168.1.1          # Aggressive scan

# Netcat
nc -lvnp 4444                # Listener start karo
nc 192.168.1.1 4444          # Connect karo

# OpenSSL
openssl enc -aes-256-cbc -base64 -k "pass" -pbkdf2 -in file.txt   # Encrypt
openssl enc -d -aes-256-cbc -base64 -k "pass" -pbkdf2 -in enc.txt # Decrypt

# Hashing
echo "text" | sha256sum      # SHA256 hash
echo "text" | md5sum         # MD5 hash
sha256sum file.txt           # File ka hash

# Log analysis
tail -f /var/log/apache2/access.log   # Apache logs
tail -f /var/log/auth.log             # Auth logs
grep "Failed" /var/log/auth.log       # Failed logins
```

---

## 📊 System Information
```bash
uname -a                     # System info
whoami                       # Current user
id                           # User ID & groups
hostname                     # System name
df -h                        # Disk space
free -h                      # RAM usage
uptime                       # System uptime
history                      # Command history
sudo !!                      # Last command sudo se chalaao
```

---

## 🔧 Service Management
```bash
sudo service apache2 start   # Service start
sudo service apache2 stop    # Service stop
sudo service apache2 restart # Service restart
sudo service apache2 status  # Service status
sudo systemctl enable ssh    # Boot par auto-start
sudo systemctl list-units    # All services list
```

---

*ApexPlanet Software Pvt. Ltd. Cybersecurity Internship — Task 1*
