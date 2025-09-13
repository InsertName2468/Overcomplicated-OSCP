## 📌 What is Hashcat?

Hashcat is one of the fastest and most versatile password-cracking tools. It allows you to recover passwords by attacking their hash values using different cracking modes (dictionary, brute-force, hybrid, etc.).

Installation:
`sudo apt install hashcat`

It supports many hash types, which you can list with:

```bash
sudo hashcat -hh
```

---
## How to use Hashcat
### Getting Started with Hashcat

#### Step 1: Obtain the Hash

To crack a password, you first need the hash of the file or data.

For example, if you want to obtain the hash of an **encrypted ZIP file** located on your Desktop:

```bash
┌──(kali㉿kali)-[~]
└─$ cd Desktop  #switch directory to Desktop or wherever your file is

┌──(kali㉿kali)-[~/Desktop]
└─$ ls -a       #make sure the file is there
. .. helloWorld.zip

┌──(kali㉿kali)-[~]
└─$ zip2john helloWorld.zip > hash.txt    #Computes the hash...
```

The output will look something like this (your hash will differ):

```bash
helloWorld.zip/helloWorld.txt:$zip2$*0*3*0*e48cebccce6fde8118e68db92ba7275b*ad06*a8*1ac6815ac84009ea2a2a2fc8c9af6248d728018ae08941bcb57159a9437cd22059202b4958bb265051f84c756*0fc7918b061b2a1ddb25*$/zip2$:hello.txt:hello.zip:helloWorld.zip
```

---
### Step 2: Identify the Hash Mode

Each hash type has a corresponding **mode ID**.  
For example, to find **WinZip** support:
```bash
┌──(kali㉿kali)-[~]
└─$ sudo hashcat -hh | grep WinZip 
   13600 | WinZip                                                     | Archive
```
so the correct mode is -m 13600

---
### Step 3: Run Hashcat

Now, use hashcat to attempt cracking the hash with a **wordlist** (e.g., `rockyou.txt` on Kali Linux):
```bash
┌──(kali㉿kali)-[~]
└─$ sudo hashcat -m 13600 hash.txt /usr/share/wordlists/rockyou.txt
```

---
### Step 4: View Cracked Passwords

After the attack, display any recovered passwords with:
```bash

┌──(kali㉿kali)-[~]
└─$ sudo hashcat -m 13600 hash.txt /usr/share/wordlists/rockyou.txt --show


```

---
## To Calculate Hash of Different Type of Files

```bash
zip2john > hash.txt #for zip files
7z2john > hash.txt  #for 7z files
pdf2john > hash.txt #for pdf files
```

---
## Performance Optimization & Advanced Usage

### 1. Enable GPU Acceleration

Hashcat runs best on GPUs.

- List available devices:
    
    `hashcat -I`
    
- Run on a specific device (e.g., GPU ID `2`):
    
    `hashcat -m <mode> hash.txt wordlist.txt -d 2`
    

---

### 2. Resume Sessions

If you stop a cracking session, you can resume it later:

`hashcat --restore`

Or save a named session:

`hashcat -m <mode> hash.txt wordlist.txt --session=mycrack`

---

### 3. Benchmark Your System

Check performance for different hash types:

`hashcat -b`

---

### 4. Use Rules for Smarter Cracking

Rules mutate words in your wordlist (e.g., adding numbers, changing case).

`hashcat -m <mode> hash.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule`

---

### 5. Hybrid Attacks

Combine dictionary + brute-force:

`hashcat -m <mode> hash.txt wordlist.txt ?d?d`

(Tries each word with 2 digits appended, like `password12`).

---

### 6. Optimize Workload

Adjust workload profiles for speed/stability:

`hashcat --workload-profile=3`

(Values: `1` = low, `4` = max).

---

### 7. Incremental Mask Attacks

Brute-force with increasing length:

`hashcat -m <mode> hash.txt ?l?l?l?l --increment`

(Starts at 1 letter, then 2, up to 4).

---

✅ **Tip:** Always start with dictionary + rules before brute-force. It’s much faster.

---

## 🛠 Troubleshooting

### 1. **No devices found/No OpenCL devices**

**Error:**

`No devices found/left`

**Fix:**

- Install GPU drivers.
    
    - NVIDIA:
        
        `sudo apt install nvidia-driver nvidia-cuda-toolkit`
        
    - AMD:
        
        `sudo apt install opencl-icd-amdgpu-pro`
        
- Verify with:
    
    `hashcat -I`
    

---

### 2. **Token length exception**

**Cause:** Hash format is wrong.  
**Fix:**

- Copy the **entire** hash, no spaces/line breaks.
- Use single quotes(') instead of double quotes(")
- Check correct mode with:
    
    `hashcat -hh | grep <hash-type>`
    

---

### 3. **Exhausted**

**Cause:** Hashcat tested the whole wordlist/mask but found nothing.  
**Fix:**

- Use a bigger wordlist.
    
- Apply **rules**.
    
- Try brute-force if format is predictable.
    

---

### 4. **Password not showing after crack**

Run:

`hashcat --show`

---

### 5. **Hashcat too slow**

**Fix:**

- Use:
    
    `hashcat --workload-profile=3 --optimized-kernel-enable`
    
- Make sure GPU is being used (not CPU).
    
- Benchmark with:
    
    `hashcat -b`
    

---

✅ **Pro Tip:** Always check the Hashcat Wiki for updated guides and solutions.

---

# 🎯 Final Notes

- Hashcat is extremely powerful — use it **ethically** (only on files you own or have permission to test).
    
- Always start with **smart attacks** (dictionary + rules) before brute-force.
    
- Optimize performance by keeping drivers up to date and leveraging GPU acceleration.