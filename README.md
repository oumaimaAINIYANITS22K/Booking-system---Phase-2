# 📌 MD5 Hash Cracking Progress Report

## 📝 Overview
This report documents the process of cracking MD5 password hashes using **Hashcat with fast wordlist-based attacks and online decryption services**. The objective was to recover plaintext passwords **only using methods that finish in a few minutes**.

**Brute-force and long-duration attacks were excluded**, as some estimated cracking times reached **years or even decades**. Instead, the focus remained on **quick wordlist attacks** and **hash lookup services**.

---

## 🔍 **Hashes Cracked So Far**
As of now, **7 out of 10 hashes have been successfully cracked**:

| Username | MD5 Hash | Cracked Password |
|----------|----------------------------------|----------------|
| whatsupdoc@looneytunes.tv | `a0e8402fe185455606a2ae870dcbc4cd` | `carrots123` |
| doho@springfieldpower.net | `d730fc82effd704296b5bbcff45f323e` | `donuts4life` |
| darkknight@gothamwatch.org | `7357ff5e652d7697723893e1a5c04d90` | `iamvengeance` |
| chimichanga@fourthwall.com | `7cb56c2b86150b79cff32eaef97f338` | `breaking4thwall` |
| iamyourfather@deathstar.gov | `706ab9fc256efabf4cb4cf9d31ddc8eb` | `darkside42` |
| genius@starkindustries.net | `d50ba4dd3fe42e17e9faa9ec29f89708` | `iamironman` |
| whysoserious@gothamchaos.net | `f158d479ee181aac68b000a60e7a3d7a` | `chaos123!` |
| **Remaining Hashes (Uncracked)** | | |
| elementary@221bbaker.uk | `12c9cef0bfb6b91c42b363b4cf02d8bb` | ❌ Not yet cracked |
| quackattack@duckburg.org | `ea261222d4867b3ebdfadbe2b35e19d5` | ❌ Not yet cracked |
| ruhroh@mysterymachine.com | `ad17fbd845000b11678ccbfc94e135b56` | ❌ Not yet cracked |

---

## 🔧 **Methods Used for Cracking**

### ✅ **1. Fast Wordlist Attack with Hashcat**
The first approach was using **Hashcat** with the **RockYou** wordlist, which contains common passwords. This method is quick and **finishes in minutes**.

```bash
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt --force
```
🎯 **Outcome**: Successfully cracked multiple passwords.

To account for **small variations in passwords**, a **rule-based attack** was used, applying common modifications to words.

```bash
hashcat -m 0 -a 0 -r /usr/share/hashcat/rules/best64.rule hashes.txt /usr/share/wordlists/rockyou.txt --force
```
🎯 **Success**: Some passwords were found with minor modifications (e.g., numbers or symbols added).

---

### ✅ **2. Online MD5 Lookup Services**
For hashes that weren’t cracked using Hashcat, **online MD5 decryption services** were used. These services work instantly if the hash is already in their database.

#### **Lookup Sites Used:**
- **[CrackStation](https://crackstation.net)**
- **[Hashes.com](https://hashes.com/en/decrypt/hash)**
- **[MD5Hashing.net](https://md5hashing.net)**
- **[HashKiller.io](https://hashkiller.io/)**
- **[MD5 Decrypt](https://md5decrypt.net/)**
- **[OnlineHashCrack](https://www.onlinehashcrack.com/)**

🎯 **Outcome**: Several passwords were found **instantly**.

---

### 🚧 **3. The Remaining Uncracked Hashes**
The last three hashes **could not be cracked** with wordlists or online lookup services.  
A **hybrid attack** was tested with a **short mask** to check if the passwords were simple.

```bash
hashcat -m 0 -a 6 hashes.txt /usr/share/wordlists/rockyou.txt ?l?l?l?l?l?l
```
⚠ **Problem**: No successful cracks.

Since **full brute-force attacks** estimated **years** to complete, they were **not attempted**.

---

## ⏳ **Final Decision: Cracking Was Not Feasible for the Remaining Hashes**
Since the remaining passwords would take **too long** to crack with brute force, it was concluded that **these hashes are either highly secure or based on uncommon words not in public wordlists**.

### **Key Takeaways:**
✅ **Online hash databases were the fastest and most efficient**  
✅ **Hashcat worked well for wordlist-based passwords and minor modifications**  
✅ **Long and complex passwords remain practically unbreakable** (without high-end hardware or significant time investment)

