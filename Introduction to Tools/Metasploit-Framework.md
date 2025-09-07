## What is Metasploit
The Metasploit Framework is an open source platform that supports vulnerability research, exploit development, and the creation of custom security tools.

How to install: `sudo apt install metasploit-framework`

---
## Introduction to the Metasploit Framework Directory
Here's a simplified metasploit framework directory:
```bash
metasploit-framework
├── data
├── documentation #stores documentations for msf
├── lib
├── plugins
├── scripts #store msf scripts, such as meterpreter
├── tools
├── modules #store msf modules
	├── auxiliary #auxiliary modules such as port scanner and password cracker
	├── exploits #exploits module
	├── payloads #scripts to execute when 
	├── post
	├── encoders
	├── evasion #evasive module used to avoid antivirus detection 
	├── nops
```
