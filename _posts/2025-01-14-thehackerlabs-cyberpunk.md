---
title: "Cyberpunk"
date: 2025-01-14 00:00:00 +0900
categories: [The Hacker Labs] 
tags: [Linux, Easy]
---

# The Hacker Labs Cyberpunk WriteUp

![cyberpunk](assets/img/pentest/cyberpunk.png)

- OS: Linux
- Difficulty: Easy
- Platform: The Hacker Labs

## Introduction

Welcome to **"Cyberpunk - Relic Infiltration,"**, a Linux-based CTF for beginners. In this writeup, we will narrate step by step how the infiltration and exploitation of vulnerabilities were carried out, from initial reconnaissance to privilege escalation and gaining **root** access.

![cyberpunk cmd](assets/img/pentest/cyberpunkcmd.png)

## Identifying Our Target

We started by identifying the IP of the target machine using the ip a command to check our network configuration, and then with arp-scan, we scanned the local network to find the IP of the vulnerable machine.

```bash
❯ ip a
```

```bash
❯ 192.168.1.134 08:00:27:d9:48:fe (Unknown)
```

## NMAP Scan

```bash
❯ sudo nmap -p- --open --min-rate 5000 -vvv -n -Pn 192.168.1.134 -oG allPorts
```

### What does this mean?

- `-p-`: Scan all ports.
- `--open`: Shows only open ports.
- `--min-rate 5000`: Minimum scan rate.
- `-vvv`: Very high verbosity for detailed information.
- `-n`: Disables DNS resolution.
- `-Pn`: Ignores host discovery (does not check if the host is online).
- `192.168.1.134`: IP address of the target machine.
- `-oG allPorts`: Saves the results to a file called "allPorts".

```bash
❯ sudo nmap -p- --open --min-rate 5000 -vvv -n -Pn 192.168.1.134 -oG allPorts
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-14 21:55 CST
Initiating ARP Ping Scan at 21:55
Scanning 192.168.1.134 [1 port]
Completed ARP Ping Scan at 21:55, 0.08s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 21:55
Scanning 192.168.1.134 [65535 ports]
Discovered open port 22/tcp on 192.168.1.134
Discovered open port 21/tcp on 192.168.1.134
Discovered open port 80/tcp on 192.168.1.134
Completed SYN Stealth Scan at 21:56, 54.57s elapsed (65535 total ports)
Nmap scan report for 192.168.1.134
Host is up, received arp-response (0.00046s latency).
Scanned at 2025-01-14 21:55:11 CST for 54s
Not shown: 53054 filtered tcp ports (no-response), 12478 closed tcp ports (reset)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE REASON
21/tcp open  ftp     syn-ack ttl 64
22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64
MAC Address: 08:00:27:D9:48:FE (PCS Systemtechnik/Oracle VirtualBox virtual NIC)

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 54.79 seconds
           Raw packets sent: 124832 (5.493MB) | Rcvd: 12484 (499.368KB)
```

Now I will use a function that I have saved in my zshrc call **extractPorts**. This will copy only the ports that I will scan. 

```bash
❯ extractPorts allPorts
───────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: extractPorts.tmp
───────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ 
   2   │ [*] Extracting information...
   3   │ 
   4   │     [*] IP Address: 192.168.1.134
   5   │     [*] Open ports: 21,22,80
   6   │ 
   7   │ [*] Ports copied to clipboard
   8   │ 
───────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```
## NMAP second scan

```bash
nmap -sVC -p21,22,80 192.168.1.134 -oN ports
```

### What does this mean?

- `-sC`: Enables version detection and vulnerability scanning.
- `-sV`: Service version scanning.
- `-p`: Scans given ports.
- `192.168.1.134`: IP address of the target machine.
- `oN`: Saves the results to a file called "ports".

```bash
 nmap -sVC -p21,22,80 192.168.1.134 -oN ports
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-14 22:15 CST
Nmap scan report for Cyberpunk.attlocal.net (192.168.1.134)
Host is up (0.00096s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| drwxr-xr-x   2 0        0            4096 May  1  2024 images
| -rw-r--r--   1 0        0             713 May  1  2024 index.html
|_-rw-r--r--   1 0        0             923 May  1  2024 secret.txt
| fingerprint-strings: 
|   GenericLines: 
|     220 Servidor ProFTPD (Cyberpunk) [::ffff:192.168.1.134]
|     Orden incorrecta: Intenta ser m
|     creativo
|     Orden incorrecta: Intenta ser m
|     creativo
|   Help: 
|     220 Servidor ProFTPD (Cyberpunk) [::ffff:192.168.1.134]
|     214-Se reconocen las siguiente 
|     rdenes (* =>'s no implementadas):
|     XCWD CDUP XCUP SMNT* QUIT PORT PASV 
|     EPRT EPSV ALLO RNFR RNTO DELE MDTM RMD 
|     XRMD MKD XMKD PWD XPWD SIZE SYST HELP 
|     NOOP FEAT OPTS HOST CLNT AUTH* CCC* CONF* 
|     ENC* MIC* PBSZ* PROT* TYPE STRU MODE RETR 
|     STOR STOU APPE REST ABOR RANG USER PASS 
|     ACCT* REIN* LIST NLST STAT SITE MLSD MLST 
|     comentario a root@Cyberpunk
|   NULL, SMBProgNeg, SSLSessionReq: 
|_    220 Servidor ProFTPD (Cyberpunk) [::ffff:192.168.1.134]
22/tcp open  ssh     OpenSSH 9.2p1 Debian 2+deb12u2 (protocol 2.0)
| ssh-hostkey: 
|   256 6d:b5:c8:65:8d:1f:8a:98:76:93:26:27:df:29:72:4a (ECDSA)
|_  256 a5:83:2a:8f:eb:c6:f1:0b:e0:e6:d8:e1:05:3b:4c:a5 (ED25519)
80/tcp open  http    Apache httpd 2.4.59 ((Debian))
|_http-title: Arasaka
|_http-server-header: Apache/2.4.59 (Debian)
```

## Enumeration

### Port 80

Upon identifying that port 80 was open during the scan, the IP address was entered into the browser. A page called **Arasaka** with an image was found.

![web](assets/img/pentest/web.png)
