# MFP Hacking: Pass-Back Attack

## What is an MFP?

**Multi-Function Peripherals (MFPs)** are network-connected printers capable of print, copy, scan, fax, and email integration. They're often overlooked in pentests but can yield:

- Credential Disclosure
- File System Access
- Memory Access

> MFPs are frequently forgotten in security maintenance = **quick wins** for attackers.

---

## Why MFPs Are Valuable Targets

MFPs integrate with corporate infrastructure via:

| Protocol | Purpose |
|----------|---------|
| **LDAP** | User authentication, email lookups, home folder access |
| **SMTP** | Scan-to-email functionality |
| **Network Shares** | File storage access |

**Key insight:** MFPs store credentials to query LDAP/SMTP servers. Capture these = network entry point.

---

## Pass-Back Attack

**Concept:** Replace the legitimate LDAP/SMTP server address with your attacker-controlled server to capture credentials.

### Attack Flow

1. Access the **Embedded Web Service (EWS)** (printer's web admin panel)
2. Navigate to LDAP/SMTP settings
3. Replace legitimate server IP with your IP
4. Set up listener to capture credentials
5. Wait for user authentication or stored credential transmission

---

## Accessing the EWS

### Default Credentials

| Vendor | Username   | Password             |
| ------ | ---------- | -------------------- |
| Ricoh  | `admin`    | *(blank)*            |
| HP     | `admin`    | `admin` or *(blank)* |
| Canon  | `ADMIN`    | `canon`              |
| Epson  | `EPSONWEB` | `admin`              |

### Tools for MFP Exploitation

| Tool | Purpose | Link |
|------|---------|------|
| **PRET** | Printer Exploitation Toolkit | github.com/RUB-NDS/PRET |
| **Praeda** | Info disclosure & code execution | github.com/percx/Praeda |

📖 Reference: [Printer Security Testing Cheat Sheet](http://www.hacking-printers.net/wiki/index.php/Printer_Security_Testing_Cheat_Sheet)

---

## Practical Example: LDAP Pass-Back

```bash
# 1. Set up Netcat listener on LDAP port
nc -lvnp 389

# 2. In EWS: Replace LDAP server (e.g., 192.168.1.100) with your IP
# 3. Save settings
# 4. Wait for user to authenticate at MFP control panel
# 5. Credentials sent to your listener
```

---

## Other Pass-Back Targets

| Service | Attack Vector |
|---------|---------------|
| **SMTP** | Replace SMTP server → capture stored email credentials |
| **Windows Sign-in** | Replace domain controller → capture domain credentials |

---

## Key Takeaways

- ✅ MFPs are often **physically accessible** and **poorly managed**
- ✅ Frequently have **default credentials**
- ✅ Store **sensitive credentials** for LDAP/SMTP/Domain auth
- ✅ **High payout, low risk** target for pentests