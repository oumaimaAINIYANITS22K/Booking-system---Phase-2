# 📌 MD5 Hash Cracking Progress Report

## 📝 Overview
This report documents the step-by-step process of cracking MD5 password hashes using **Hashcat, online decryption services, and wordlist-based attacks**. The objective was to recover plaintext passwords from a set of hashed credentials.

Initially, **Hashcat was used with wordlists and brute-force attacks**, but as the process progressed, it became evident that **some hashes required an unreasonable amount of time to crack**—with estimates reaching up to **33 years** in some cases. As a result, **online hash lookup services were used to speed up the process**, leading to multiple successful cracks.

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
### ✅ **1. Initial Attempts with Hashcat**
At first, **Hashcat** was used with **common wordlists**, including **RockYou** and **SecLists**:
```bash
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt --force
```
🎯 **Outcome**: This cracked some passwords, but not all.

To account for **variations in password formats**, a **rule-based attack** was attempted:
```bash
hashcat -m 0 -a 0 -r /usr/share/hashcat/rules/best64.rule hashes.txt /usr/share/wordlists/rockyou.txt --force
```
🎯 **Success**: Discovered passwords with minor modifications (e.g., added numbers or symbols).

---

### ✅ **2. Transition to Online Hash Lookup**
After **Hashcat failed to crack some hashes**, we turned to **online MD5 decryption services**, including:
- **[CrackStation](https://crackstation.net)**
- **[Hashes.com](https://hashes.com/en/decrypt/hash)**
- **[MD5Hashing.net](https://md5hashing.net)**
- **[HashKiller.io](https://hashkiller.io/)**
- **[MD5 Decrypt](https://md5decrypt.net/)**
- **[OnlineHashCrack](https://www.onlinehashcrack.com/)**

🎯 **Outcome**: Several passwords were found **instantly** in these databases.

---

### 🚧 **3. The Final Challenge: Remaining Hashes Were Too Strong**
Three hashes **could not be cracked** using any of the above methods.  
To test **brute-force feasibility**, a **hybrid attack** was attempted:
```bash
hashcat -m 0 -a 6 hashes.txt /usr/share/wordlists/rockyou.txt ?l?l?l?l?l?l
```
⚠ **Problem**: The estimated cracking time was **several years**.

A **full brute-force** attempt for **14-16 lowercase characters** was also started:
```bash
hashcat -m 0 -a 3 hashes.txt ?l?l?l?l?l?l?l?l?l?l?l?l?l?l --force
```
⏳ **Time Estimate**: Over **33 years** on standard hardware.  
📌 **Conclusion**: Not practical to complete.

---

## ⏳ **Final Decision: Cracking Was Not Feasible**
Since the remaining passwords would take **decades** to crack with brute force, it was concluded that **these hashes are either highly secure, or based on long, uncommon words that aren’t in any public wordlist**.

### **Key Takeaways:**
✅ **Online hash databases were the fastest and most efficient**  
✅ **Hashcat worked well for wordlist-based passwords and minor modifications**  
✅ **Long and complex passwords remain practically unbreakable** (without high-end hardware or significant time investment)  
