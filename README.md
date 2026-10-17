🇺🇸 English | 🇧🇷 [Português](README.pt-BR.md)

# OverTheWire: Bandit Writeups

## Overview

This repository documents the completion of all 34 levels of **OverTheWire: Bandit**, a sequence of hands-on challenges in basic offensive security on a Linux environment. Each level requires finding a configuration, permission, or encoding flaw to gain access to the next one, using command-line tools such as `grep`, `find`, `netcat`, `openssl`, `cron`, and `nmap`.

---

## ⚠️ Responsible Use & Educational Policy

This repository is developed strictly for educational purposes, technical methodology auditing, and personal competency tracking. In compliance with the pedagogical objectives of the wargame community:

* **Data Sanitization:** All final authentication tokens, flags, and credentials are strictly sanitized and omitted (`[REDACTED]`).
* **Anti-Spoilers:** The solutions are structured to demonstrate system architecture, logic gates, and command pipelines. Users are strongly encouraged to use this material as a reference framework *after* attempting the challenges independently. Copying commands without active cognitive analysis defeats the learning purpose.

---

## 🗺️ Repository Index

| Writeup File | Core Conceptual Focus | Status |
| :--- | :--- | :--- |
| [**levels-00-07.md**](./levels-00-07.md) | Fundamentals, File System Navigation, Object Properties & Special Filenames | `Completed` |
| [**levels-07-13.md**](./levels-07-13.md) | Stream Redirection, Data Processing, Encoding & Compression Utilities | `Completed` |
| [**levels-13-19.md**](./levels-13-19.md) | Networking Architecture, SSH Remote Sessions & Shell Execution Hooks | `Completed` |
| [**levels-19-27.md**](./levels-19-27.md) | Setuid Exploitation, Local Privilege Escalation, Scripting Automation & Shell Escapes | `Completed` |
| [**levels-27-33.md**](./levels-27-33.md) | Git Repository Exploitation & Restricted Environment Escapes | `Completed` |

---

## 🧠 Core Engineering Competencies

* **File System Auditing:** Deep validation of object attributes, permissions matrix, hidden allocations, and handling of malformed/dash-prefixed filenames.
* **Data Processing Pipelines:** Compounding string manipulation utilities to execute high-efficiency filtering, parsing, and stream parsing on dense data targets.
* **Cryptographic & Network Logistics:** Mapping remote systems, operating secure terminal connections via asymmetric keys, and debugging raw data flows across network sockets.
* **Privilege Escalation & Automation Auditing:** Auditing scheduled system routines (cron jobs), exploiting `setuid` binary misconfigurations, and engineering bash scripts to automate network brute-forcing payloads.
* **Version Control Diagnostics & Shell Evasion:** Reverse engineering Git repository histories (unmerged branches, detached commits, submodules) and bypassing strict input-filtering shells via internal parameter expansion (`$0`).