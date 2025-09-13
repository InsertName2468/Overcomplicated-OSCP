# 📝 Hashcat Cheat Sheet

### 🔍 General Info

- List all hash modes:
    
    `hashcat -hh`
    
- Benchmark performance:
    
    `hashcat -b`
    
- List devices (CPU/GPU):
    
    `hashcat -I`
    

---

### 📂 Obtaining Hashes

- From a ZIP file:
    
    `zip2john file.zip > hash.txt`
    
- From a PDF:
    
    `pdf2john.pl file.pdf > hash.txt`
    
- From a Windows hash dump (SAM/NTLM):
    
    `samdump2 SYSTEM SAM > hash.txt`
    

---

### ⚡ Basic Cracking

- Dictionary attack:
    
    `hashcat -m <mode> hash.txt wordlist.txt`
    
- Show cracked passwords:
    
    `hashcat -m <mode> hash.txt wordlist.txt --show`
    
- Resume a session:
    
    `hashcat --restore`
    

---

### 🧩 Attack Modes

- Dictionary + Rule (mutations):
    
    `hashcat -m <mode> hash.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule`
    
- Brute-force (example: 6 lowercase letters):
    
    `hashcat -m <mode> hash.txt ?l?l?l?l?l?l`
    
- Hybrid (dictionary + numbers):
    
    `hashcat -m <mode> hash.txt wordlist.txt ?d?d`
    

---

### 🎛 Optimization

- Use GPU only:
    
    `hashcat -m <mode> hash.txt wordlist.txt -d 2`
    
- Increase performance (profile 3 = balanced):
    
    `hashcat -m <mode> hash.txt wordlist.txt --workload-profile=3`
    
- Save session:
    
    `hashcat -m <mode> hash.txt wordlist.txt --session=mycrack`
    

---

### 🛠 Troubleshooting Quick Fixes

- **No devices found:** Install GPU drivers → `hashcat -I`
    
- **Token length exception:** Check hash format & mode
    
- **Exhausted:** Try bigger wordlist/rules
    
- **Password not showing:** Run `--show`
    

---
