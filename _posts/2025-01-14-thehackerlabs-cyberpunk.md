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
sudo nmap -p- --open -sS -sC -sV --min-rate 5000 -vvv -n -Pn 192.168.1.134 -oG allPorts
```

### What does this mean?

`-p-`: Scan all ports.
`--open`: Shows only open ports.
`-sS`: SYN scan to determine the status of the ports.
`-sC`: Enables version detection and vulnerability scanning.
`-sV`: Service version scanning.
`--min-rate 5000`: Minimum scan rate.
`-vvv`: Very high verbosity for detailed information.
`-n`: Disables DNS resolution.
`-Pn`: Ignores host discovery (does not check if the host is online).
`192.168.1.134`: IP address of the target machine.
`-oG allPorts`: Saves the results to a file called "allPorts".