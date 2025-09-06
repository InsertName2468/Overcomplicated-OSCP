# Kali Linux Cheat Sheet for Beginners

A beginner-friendly cheat sheet for essential Kali Linux commands, with real-world examples to help you navigate, manage your system, and get started with penetration testing and ethical hacking.

---

## 📁 File & Directory Navigation

|Command|Description|Example|
|---|---|---|
|`ls`|List directory contents|`ls`|
|`ls -la`|List all files (including hidden) in long format|`ls -la`|
|`cd <dir>`|Change directory|`cd /etc`|
|`cd ..`|Go up one directory level|`cd ..`|
|`cd -`|Switch to previous directory|`cd -`|
|`pwd`|Print working directory|`pwd` → `/home/kali`|
|`mkdir <dir>`|Create a new directory|`mkdir testdir`|
|`rm <file>`|Delete a file|`rm file.txt`|
|`rm -r <dir>`|Remove directory and its contents|`rm -r testdir/`|
|`cp <src> <dest>`|Copy files/directories|`cp file.txt /tmp/`|
|`mv <src> <dest>`|Move or rename files|`mv file.txt file_old.txt`|
|`touch <file>`|Create an empty file|`touch new.txt`|
|`cat <file>`|Display file contents|`cat /etc/passwd`|
|`nano <file>`|Open file in Nano editor|`nano script.sh`|
|`find / -name <file>`|Search for a file by name|`find / -name passwd`|
|`locate <file>`|Fast file search (requires `mlocate`)|`locate sshd_config`|
|`tree`|Show directory structure|`tree /etc`|

---

## 👤 User & Group Management

|Command|Description|Example|
|---|---|---|
|`whoami`|Show current user|`whoami` → `kali`|
|`id`|Show user ID and groups|`id`|
|`groups <user>`|Show groups a user belongs to|`groups kali`|
|`adduser <username>`|Add new user|`adduser hacker1`|
|`passwd <username>`|Change user password|`passwd hacker1`|
|`usermod -aG <group> <user>`|Add user to a group|`usermod -aG sudo hacker1`|
|`su <user>`|Switch to another user|`su hacker1`|
|`sudo -l`|Show available sudo privileges|`sudo -l`|
|`logout`|End session|`logout`|

---

## 🔍 System Information & Monitoring

|Command|Description|Example|
|---|---|---|
|`uname -a`|Show system/kernel info|`uname -a`|
|`lsb_release -a`|Show Linux distro details|`lsb_release -a`|
|`cat /etc/os-release`|Display OS information|`cat /etc/os-release`|
|`hostname`|Show hostname|`hostname`|
|`uptime`|Show uptime and load|`uptime`|
|`df -h`|Disk usage (human readable)|`df -h`|
|`free -m`|Memory usage in MB|`free -m`|
|`ps aux`|Show running processes|`ps aux`|
|`top`|Real-time process monitor|`top`|
|`htop`|Interactive process viewer|`htop`|
|`dmesg`|Kernel messages (boot/logs)|`dmesg|
|`journalctl -xe`|Show system logs|`journalctl -xe`|

---

## 📡 Networking & Reconnaissance

|Command|Description|Example|
|---|---|---|
|`ip a`|Show IP addresses|`ip a`|
|`ifconfig`|Legacy command for interfaces|`ifconfig`|
|`ping <host>`|Test connectivity|`ping google.com`|
|`traceroute <host>`|Trace route packets take|`traceroute 8.8.8.8`|
|`dig <domain>`|DNS lookup|`dig example.com`|
|`nslookup <domain>`|Legacy DNS query|`nslookup example.com`|
|`arp -a`|Show ARP table|`arp -a`|
|`netstat -tuln`|Show open ports|`netstat -tuln`|
|`ss -tuln`|Show open ports (faster)|`ss -tuln`|
|`nc -lvnp <port>`|Open netcat listener|`nc -lvnp 4444`|
|`nmap <ip>`|Scan for open ports|`nmap 192.168.1.1`|
|`wget <url>`|Download from internet|`wget http://example.com/file.txt`|
|`curl <url>`|Fetch webpage|`curl http://example.com`|

---

## 🔐 Permissions & Ownership

|Command|Description|Example|
|---|---|---|
|`ls -l`|Show file permissions|`ls -l`|
|`chmod <mode> <file>`|Change permissions (numeric)|`chmod 755 script.sh`|
|`chmod u+x <file>`|Add execute permission (symbolic)|`chmod u+x run.sh`|
|`chown <user>:<group> <file>`|Change ownership|`chown kali:kali file.txt`|
|`umask`|Show default permissions mask|`umask`|
|`getfacl <file>`|Show extended ACL permissions|`getfacl file.txt`|
|`setfacl -m u:user:rwx <file>`|Set ACL for a user|`setfacl -m u:hacker:r file.txt`|

---

## 🧪 Package Management (APT & DPKG)

|Command|Description|Example|
|---|---|---|
|`sudo apt update`|Update package index|`sudo apt update`|
|`sudo apt upgrade`|Upgrade packages|`sudo apt upgrade`|
|`sudo apt full-upgrade`|Upgrade, handling dependencies|`sudo apt full-upgrade`|
|`sudo apt install <pkg>`|Install a package|`sudo apt install nmap`|
|`sudo apt remove <pkg>`|Remove a package|`sudo apt remove nmap`|
|`apt search <pkg>`|Search for package|`apt search wireshark`|
|`dpkg -i <deb>`|Install .deb package|`dpkg -i file.deb`|
|`dpkg -l`|List installed packages|`dpkg -l|
|`sudo apt --fix-broken install`|Fix broken dependencies|`sudo apt --fix-broken install`|

---

## 🧰 Essential Hacking Tools

|Tool|Description|Example|
|---|---|---|
|`nmap`|Network scanner|`nmap -sV 192.168.1.1`|
|`hydra`|Password brute forcing|`hydra -l admin -P rockyou.txt 192.168.1.1 ssh`|
|`sqlmap`|Automated SQL injection|`sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs`|
|`john`|Password cracker|`john --wordlist=rockyou.txt hashes.txt`|
|`wireshark`|GUI traffic analyzer|`wireshark`|
|`msfconsole`|Metasploit Framework|`msfconsole`|
|`burpsuite`|Web proxy/scanner|`burpsuite`|
|`aircrack-ng`|Wireless cracking suite|`aircrack-ng capture.cap`|
|`gobuster`|Directory brute force|`gobuster dir -u http://example.com -w wordlist.txt`|
|`nikto`|Web vulnerability scanner|`nikto -h http://example.com`|
|`enum4linux`|Enumerate Windows shares|`enum4linux -a 192.168.1.10`|
|`dirb`|Directory brute forcing|`dirb http://example.com`|

---

## 🔄 Other Useful Commands

|Command|Description|Example|
|---|---|---|
|`clear`|Clear screen|`clear`|
|`history`|Show command history|`history`|
|`alias`|Create command shortcut|`alias ll='ls -la'`|
|`echo <text>`|Print to terminal|`echo Hello Kali`|
|`tar -czf <file>.tar.gz <dir>`|Compress files|`tar -czf backup.tar.gz Documents/`|
|`tar -xzf <file>.tar.gz`|Extract archive|`tar -xzf backup.tar.gz`|
|`zip -r <file>.zip <dir>`|Create zip archive|`zip -r files.zip Documents/`|
|`unzip <file>.zip`|Extract zip|`unzip files.zip`|
|`scp <src> <user>@<ip>:<dest>`|Secure file copy|`scp file.txt user@192.168.1.10:/tmp/`|
|`rsync -avz <src> <dest>`|Sync files efficiently|`rsync -avz /home/kali/ root@192.168.1.1:/backup/`|
|`man <cmd>`|Show manual|`man nmap`|
|`exit`|Exit terminal|`exit`|

---

## 🧠 Keyboard Shortcuts

|Shortcut|Description|
|---|---|
|`Ctrl + C`|Cancel a running command|
|`Ctrl + Z`|Suspend current process|
|`fg`|Resume last suspended process|
|`Ctrl + R`|Search command history|
|`Ctrl + L`|Clear terminal|
|`Ctrl + D`|Logout/exit terminal|
|`TAB`|Auto-complete commands/files|
|`↑ / ↓`|Navigate history|

---

## ✅ Common Use Cases

### 🔎 Scan a target with Nmap

`nmap -sV -T4 192.168.1.100`

### 💣 Brute-force SSH login with Hydra

`hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.100`

### 🕷️ Run SQL Injection with sqlmap

`sqlmap -u "http://example.com/index.php?id=1" --dbs`

### 🧬 Crack password hash with John

`john --wordlist=rockyou.txt hashes.txt`

---

## 📖 Manual (man)

Kali Linux has *a LOT* of tools. Over 600, in fact. It’s impossible to memorize every function and syntax. Use the built-in manual with `man`:

`man nmap`

or you could also visi the [Kali Tool Documentation][kali.org/tools] , ask an AI even [Google][google.com] it! Remember, don't stress yourself, just take it easy!

---

## ⚡ Best Practices & Safety

- **Update often:** `sudo apt update && sudo apt upgrade`
    
- **Use root only when needed** → work as a normal user, switch to root with `sudo su`
    
- **Be cautious with destructive commands** (`rm -rf /`)
    
- **Always test on lab environments** before running tools on production systems
    
- **Check logs when troubleshooting** → `dmesg`, `journalctl`, `systemctl status`