# 🔐 Offensive-Security-Journal

![Security](https://img.shields.io/badge/Focus-Offensive_Security-red?style=for-the-badge)
![Platform](https://img.shields.io/badge/Labs-TryHackMe_&_Cisco-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## 📖 Overview
This repository serves as my technical "Knowledge Base" and laboratory journal. It documents my progress through various offensive security certifications and platforms. My goal is to master the **cyber kill chain**, from initial reconnaissance to post-exploitation and reporting.

> [!NOTE]
> Every entry here represents a "lesson learned" from a real-world scenario or a controlled lab environment.

---

## 🛠 Methodology & Topics

### 🔍 1. Reconnaissance & Enumeration
* **Active Discovery:** Advanced `Nmap` scripting (NSE), `Netcat` banner grabbing.
* **Protocol Analysis:** Deep dives into insecure legacy protocols:
    * **SMB:** Null sessions, enumeration with `enum4linux`.
    * **FTP:** Anonymous access, buffer overflows, and cleartext sniffing.
    * **Telnet/HTTP:** Traffic analysis using `tcpdump` and `Wireshark`.

### 🧨 2. Exploitation
* **Initial Access:** Utilizing `Metasploit Framework` and manual exploit modification.
* **Payload Delivery:** Crafting reverse shells via `Bash`, `Python`, and `Netcat`.

### 📈 3. Post-Exploitation & PrivEsc
* **Linux Privilege Escalation:**
    * Exploiting misconfigured `SUDO` rights.
    * Abusing `SUID` binaries (GTFOBins).
    * Kernel exploits and Cron job manipulation.

---

## 📁 Repository Structure

```bash
.
├── 📂 Network-Security
│   ├── insecure-protocols.md    # Analysis of SMB, FTP, Telnet
│   └── enumeration-cheatsheet.md # Nmap & Gobuster flags
├── 📂 Linux-PrivEsc
│   ├── sudo-abuse.md           # Documentation on NOPASSWD vulnerabilities
│   └── suid-exploitation.md     # Findings on unusual binary permissions
├── 📂 Write-ups
│   └── TryHackMe-Labs/          # Detailed walkthroughs of completed rooms
└── 📂 Scripts
    └── recon-automator.sh       # Custom Bash scripts for initial recon

```

---

## 🚀 Key Learning Milestones

* **[Date]**: Completed the "Junior Penetration Tester" path on TryHackMe.
* **[Date]**: Successfully performed manual Linux Privilege Escalation on a hardened lab machine.
* **[Date]**: Documented the "Insecure Protocols" series for the Oxford Saïd research project.

---

## 🧪 Lab Environment

My research is conducted using:

* **OS:** Kali Linux / Parrot OS
* **Virtualization:** VMware / VirtualBox
* **Hardware:** Raspberry Pi (for network monitoring)

---

## ⚠️ Legal Disclaimer

The content of this repository is for **educational purposes only**. All testing is performed on systems I own or have explicit written permission to test. Unauthorized access to computer systems is illegal.

---

**Current Status:** 🟢 Actively Updating

```

---

### 💡 Why this works for you:

1.  **The Directory Tree:** Showing the `bash` structure of your folders makes you look organized. It tells a recruiter, "This person has a system for their work."
2.  **Focus on Methodology:** You aren't just listing tools; you are listing *concepts* (e.g., "Abusing SUID binaries," "Null sessions"). This shows you understand the underlying theory.
3.  **The "Key Milestones" Section:** This acts as a mini-timeline of your growth. It’s very satisfying for someone browsing your profile to see your progress over time.
4.  **The Disclaimer:** In the security world, a clear disclaimer is a sign of a professional, "white-hat" mindset.

---

**Next Step:** Would you like me to help you create a specific **"Enumeration Cheatsheet"** template in Markdown that you can use as your first major file in this journal?

```
