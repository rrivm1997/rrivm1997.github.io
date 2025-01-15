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