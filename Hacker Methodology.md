# The 5 Stages of Ethical Hacking

### 1. Reconnaissance (Information Gathering)

_The process of collecting data about the target to identify entry points. This is primarily **Passive Recon** (OSINT)._

- **Goal:** Understand the target layout regarding people, technology, and infrastructure.
- **Techniques:**
    - Reviewing publicly available information (Social Media, LinkedIn).
    - Examining DNS records and subdomains (Whois, nslookup).
    - Browsing target websites for tech stacks (Wappalyzer).
- **Key Concept:** _The more potential entry points found here, the higher the chance of success later._

### 2. Scanning & Enumeration

_The transition to **Active Recon** where the hacker directly interacts with the system._

- **Goal:** Discover open ports, running services, and specific vulnerabilities.
- **Techniques:**
    - **Port Scanning:** Identifying open doors (e.g., Nmap).
    - **Network Mapping:** Visualizing the topology.
    - **Vulnerability Scanning:** Automated checks for known CVEs.
- **PNPT Note:** _In the PNPT, enumeration is the most critical skill. If you get stuck, you likely missed something in this step._

### 3. Gaining Access (Exploitation)

_The phase where vulnerabilities found during scanning are weaponized._

- **Goal:** Bypass security controls to gain unauthorized entry.
- **Techniques:**
    - **Password Cracking:** Brute-force or dictionary attacks.
    - **Social Engineering:** Phishing or physical pretexting.
    - **Exploitation:** specific payloads for unpatched software (Metasploit, manual scripts).

### 4. Maintaining Access (Persistence)

_Ensuring access remains available even if the system is rebooted or credentials change._

- **Goal:** Establish a foothold to exfiltrate data or pivot to other systems.
- **Techniques:**
    - **Backdoors:** Installing Rootkits or Trojans.
    - **C2 (Command & Control):** Setting up remote access tools.
    - **Privilege Escalation:** Moving from standard user to Admin/Root.

### 5. Covering Tracks

_The process of hiding the intrusion to remain undetected._

- **Goal:** Remove evidence of the compromise and return the system to its original state.
- **Techniques:**
    - Deleting or modifying system/event logs.
    - Removing uploaded tools or scripts.
    - Hiding fles (Steganography or hidden directories).