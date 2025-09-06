# Kali Linux Cheat Sheet for Beginners (With Examples)

A beginner-friendly cheat sheet for basic Kali Linux commands with real examples to help you get started with penetration testing and ethical hacking.

## 📁 File & Directory Commands

| Command | Description | Example |
|--------|-------------|---------|
| `ls` | List directory contents | `ls` |
| `ls -la` | List all files (including hidden) in long format | `ls -la` |
| `cd <dir>` | Change to directory | `cd /etc` |
| `pwd` | Print working directory | `pwd` → `/home/kali` |
| `mkdir <dir>` | Create a directory | `mkdir testdir` |
| `rm <file>` | Delete a file | `rm file.txt` |
| `rm -r <dir>` | Remove directory and contents | `rm -r testdir/` |
| `cp <src> <dest>` | Copy files or directories | `cp file.txt /tmp/` |
| `mv <src> <dest>` | Move or rename files/directories | `mv file.txt file_old.txt` |
| `touch <file>` | Create empty file | `touch new.txt` |
| `cat <file>` | Display file contents | `cat /etc/passwd` |
| `nano <file>` | Open file in Nano text editor | `nano script.sh` |

## 👤 User Management

| Command | Description | Example |
|--------|-------------|---------|
| `whoami` | Current user | `whoami` → `kali` |
| `id` | Show user ID and group ID | `id` |
| `adduser <username>` | Add new user | `adduser hacker1` |
| `passwd <username>` | Change user password | `passwd hacker1` |
| `su` | Switch user | `su hacker1` |
| `logout` | End current session | `logout` |

## 🔍 System Information

| Command    | Description                               |
| ---------- | ----------------------------------------- |
| `uname -a` | System/kernel info                        |
| `hostname` | Display hostname                          |
| `uptime`   | Show uptime                               |
| `top`      | Real-time process monitor                 |
| `htop`     | Interactive process viewer (if installed) |
| `df -h`    | Disk usage in human-readable format       |
| `free -m`  | Memory usage in MB                        |

## 📡 Networking

| Command | Description | Example |
|--------|-------------|---------|
| `ip a` | Show IP addresses | `ip a` |
| `ifconfig` | Legacy command for network interfaces | `ifconfig` |
| `ping <host>` | Ping a host | `ping google.com` |
| `netstat -tuln` | Show open ports | `netstat -tuln` |
| `ss -tuln` | Show open ports (faster) | `ss -tuln` |
| `nmap <ip>` | Scan IP for open ports | `nmap 192.168.1.1` |
| `wget <url>` | Download file from internet | `wget http://example.com/file.txt` |
| `curl <url>` | Display content of a webpage | `curl http://example.com` |

## 🔐 Permissions

| Command | Description | Example |
|--------|-------------|---------|
| `chmod <mode> <file>` | Change permissions | `chmod 755 script.sh` |
| `chown <user>:<group> <file>` | Change owner of file | `chown kali:kali file.txt` |
| `ls -l` | Show file permissions | `ls -l` |

## 🧪 Package Management (APT)

| Command | Description | Example |
|--------|-------------|---------|
| `sudo apt update` | Update package index | `sudo apt update` |
| `sudo apt upgrade` | Upgrade all packages | `sudo apt upgrade` |
| `sudo apt install <package>` | Install a package | `sudo apt install nmap` |
| `sudo apt remove <package>` | Remove a package | `sudo apt remove nmap` |
| `apt search <package>` | Search for a package | `apt search wireshark` |

## 🧰 Useful Hacking Tools in Kali

| Tool | Description | Example |
|------|-------------|---------|
| `nmap` | Network scanner | `nmap -sV 192.168.1.1` |
| `hydra` | Password brute forcing | `hydra -l admin -P passwords.txt 192.168.1.1 ssh` |
| `sqlmap` | Automated SQL injection | `sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs` |
| `john` | Password cracker | `john --wordlist=passwords.txt hash.txt` |
| `wireshark` | GUI network traffic analyzer | `wireshark` |
| `msfconsole` | Metasploit Framework | `msfconsole` |
| `burpsuite` | Web proxy and scanner | `burpsuite` |

## 🔄 Other Useful Commands

| Command | Description | Example |
|--------|-------------|---------|
| `clear` | Clear terminal screen | `clear` |
| `history` | Show command history | `history` |
| `man <command>` | Manual page for a command | `man nmap` |
| `exit` | Exit terminal | `exit` |

## 🧠 Helpful Keyboard Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Ctrl + C` | Cancel a running command |
| `Ctrl + L` | Clear terminal screen |
| `Ctrl + D` | Logout or end terminal |
| `TAB` | Auto-complete commands/files |
| `↑ / ↓` | Scroll through command history |

## ✅ Common Use Cases

### 🔎 Scan a target with Nmap
```bash
nmap -sV -T4 192.168.1.100
💣 Brute-force SSH login with Hydra
bash
Copy code
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.100
🕷️ Run SQL Injection with sqlmap
bash
Copy code
sqlmap -u "http://example.com/index.php?id=1" --dbs
🧬 Crack password hash with John
bash
Copy code
john --wordlist=rockyou.txt hashes.txt ```
