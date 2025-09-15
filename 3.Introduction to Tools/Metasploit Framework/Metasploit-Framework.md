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
	├── encoders #encodes payloads to decrease the probability of being detected
	├── evasion #evasive module used to avoid antivirus detection 
	├── nops
```

---
## Metasploit Framework Commands
Here's a list of common used MSF commands
`help` / `?` : Displays the help menu
```bash
msf > show <module> : #Shows the modules such as exploits, auxiliary and payloads
show all       show encoders     show options     show plugin     show auxiliary
show exploits  show nops         show post 
```
`search <query>` : Used to search certain keywords
`use` : Use a module from the search query or directly by its name
`favorite` : Adds a module to favorite list 
`favorites` : Prints the favorite list
