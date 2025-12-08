# Penetration Testing Report: MD5 Hash Cracking Exercise

## 1. Executive Summary

This report details the process of cracking eleven MD5 password hashes extracted from a simulated, non-production database. The objective was to demonstrate proficiency in password auditing techniques, specifically hash cracking. Of the eleven hashes, one was cracked using an online reverse lookup service, and the remaining four vulnerable hashes were successfully compromised using the Hashcat tool with a dictionary attack strategy. The remaining six hashes were not compromised within the scope of this exercise.

| Cracked Hashes | Method Used |
| :---: | :---: |
| 1 | Online Hash Lookup Service (Reverse Search) |
| 4 | Hashcat + Dictionary Attack (rockyou.txt) |

---

## 2. Cracking Process & Results

The target hashes were provided in a text file (`hashes_md5.txt`) and were identified as pure MD5 hashes (Hashcat Mode: 0). The primary tool utilized was Hashcat, running dictionary and rule-based attacks against the popular `rockyou.txt` wordlist.

### 2.1. Hash 1: Online Reverse Lookup

The first attempt involved checking a public, online hash lookup service. This service maintains a large database of previously cracked hash-plaintext pairs.

* **Target Hash:** `f158d479ee181aac68b000a60e7a3d7a`
* **Cracked Password:** chaos123!
* **Explanation:** This method is the fastest way to crack common passwords, demonstrating the severe weakness of MD5 and its susceptibility to pre-computation attacks.

**Screenshot 1: Online Lookup Result**

<img width="1320" height="671" alt="Capture d&#39;écran 2025-12-08 225753" src="https://github.com/user-attachments/assets/0e55467a-66ca-4930-be8e-b08b4cb743d0" />

### 2.2. Hashes 2–5: Hashcat Dictionary Attack

The remaining hashes were processed using Hashcat with the `rockyou.txt` wordlist. The following command was used:

```bash
.\hashcat.exe -a 0 -m 0 hashes_md5.txt rockyou.txt --force
```
#### Hash 2:

* **Target Hash:** `a0e8402fe185455606a2ae870dcbc4cd`
* **Cracked Password:** carrots123
* **Explanation:** This password was likely a common word or phrase present in the extensive `rockyou.txt` wordlist, demonstrating a lack of complexity by the user.

#### Hash 3:

* **Target Hash:** `d730fc82effd704296b5bbcff45f323e`
* **Cracked Password:** donuts4life
* **Explanation:** This password was likely a common word or phrase present in the extensive `rockyou.txt` wordlist, demonstrating a lack of complexity by the user.

#### Hash 4:

* **Target Hash:** `706ab9fc256efabf4cb4cf9d31ddc8eb`
* **Cracked Password:** darkside42
* **Explanation:** This password was likely a common word or phrase present in the extensive `rockyou.txt` wordlist, demonstrating a lack of complexity by the user.


#### Hash 5:

* **Target Hash:** `d50ba4dd3fe42e17e9faa9ec29f89708`
* **Cracked Password:** iamironman
* **Explanation:** This password was likely a common word or phrase present in the extensive `rockyou.txt` wordlist, demonstrating a lack of complexity by the user.

<img width="1155" height="133" alt="Capture d&#39;écran 2025-12-08 230531" src="https://github.com/user-attachments/assets/497ebe4c-7015-47dc-ad6f-a80bfe722f30" />

## 3. Answers to questions.

### Main Difference Between Dictionary and Non-Dictionary Attacks
- Dictionary attacks try passwords from a predefined list of likely words or passwords, so they are fast but limited to that list.
- Non-dictionary (brute-force) attacks try all possible character combinations, so they are slower but can eventually find any password.

### Advantage of Access to Database with Users and Password Hashes
- The attacker can run offline cracking, testing unlimited password guesses against the hashes without lockouts or alerts.
- This makes it much easier to recover weak, reused, or short passwords from the stored hashes.

### Security Benefits of Longer Passwords
- Longer passwords create far more possible combinations, so brute-force attacks take exponentially more time and computing power.
- They are less likely to appear in password dictionaries and are harder to crack with rainbow tables or similar precomputed attacks.
