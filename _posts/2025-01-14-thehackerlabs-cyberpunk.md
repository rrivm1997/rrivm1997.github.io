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

# Introduction

Welcome to **"Cyberpunk - Relic Infiltration,"**, a Linux-based CTF for beginners. In this writeup, we will narrate step by step how the infiltration and exploitation of vulnerabilities were carried out, from initial reconnaissance to privilege escalation and gaining **root** access.

![cyberpunk cmd](assets/img/pentest/cyberpunkcmd.png)

# Identifying Our Target

We started by identifying the IP of the target machine using the ip a command to check our network configuration, and then with arp-scan, we scanned the local network to find the IP of the vulnerable machine.

```bash
❯ ip a
```

```bash
❯ 192.168.1.134 08:00:27:d9:48:fe (Unknown)
```

# NMAP Scan

```bash
❯ sudo nmap -p- --open --min-rate 5000 -vvv -n -Pn 192.168.1.134 -oG allPorts
```

### What does this mean?

- `-p-`: Scan all ports.
- `--open`: Shows only open ports.
- `-sS`: SYN scan to determine the status of the ports.
- `-sC`: Enables version detection and vulnerability scanning.
- `-sV`: Service version scanning.
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