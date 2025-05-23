# Vulnversity – TryHackMe Report

> ⚠️ WARNING: This report contains spoilers and technical solutions. Intended for educational use only.

## 🖥️ Machine Information

- **Name**: Vulnversity
- **Difficulty**: Easy
- **Tags**: Enumeration, Exploitation, File Upload, Shell Access
- **Link**: [https://tryhackme.com/room/vulnversity](https://tryhackme.com/room/vulnversity)

---

## 🔎 Enumeration

### 🔹 Nmap Scan

<details>
<summary>View nmap command and results</summary>

```bash
nmap -sCV -oN nmap.txt 10.10.10.10
```

- Open Ports:
  - 21 – FTP
  - 22 – SSH
  - 139, 445 – SMB
  - 3128 – HTTP-Proxy 
  - 3333 – HTTP (Custom Web Service)

</details>

### 🔹 Web Enumeration

- Accessed `http://10.10.10.10:3333`
- Found an upload form
- No file type restrictions in frontend

---

## 🛠️ Exploitation

<details>
<summary>Show exploitation steps (Spoiler)</summary>

1. Used `gobuster` to enumerate directories: found `/internal`
2. Tried uploading a PHP reverse shell (`php-reverse-shell.php` from Pentestmonkey)
3. Bypassed filter by renaming to `.phtml`
4. Set up listener with `nc -lvnp 4444`
5. Gained shell as `www-data`

</details>

---

## 🧗 Privilege Escalation

<details>
<summary>Show privesc steps (Spoiler)</summary>

1. Transferred `linpeas.sh` to the target and ran it
2. Found `cap_setuid` capability on a binary `/bin/bash`
3. Used it to spawn a root shell:
```bash
./bash -p
```

</details>

---

## 📚 Lessons Learned

- How file upload restrictions can be bypassed with extensions like `.php.jpg`
- Use of gobuster to discover hidden directories
- Linux capabilities can lead to privilege escalation

---

## 🧩 Flags

> ❌ Real flags are not included.  
> Root and user flags were retrieved from respective home directories.

---

*Report created by Iván | GitHub: https://github.com/Z3l1on*