### 📂 File Transfer & Management

|Port|Proto|Service|PNPT/Pentest Context|
|---|---|---|---|
|**20/21**|TCP|**FTP**|File Transfer. Watch for **anonymous login** and clear-text credentials.|
|**69**|UDP|**TFTP**|Trivial FTP. No auth required; often used to upload/download configs.|
|**990**|TCP|**FTPS**|FTP over SSL. Encrypted channel.|

### 🖥️ Remote Access

|Port|Proto|Service|PNPT/Pentest Context|
|---|---|---|---|
|**22**|TCP|**SSH**|Secure Shell. Secure remote access. Common target for **brute-forcing**.|
|**23**|TCP|**Telnet**|Unencrypted remote access. **Credentials sent in clear-text**.|
|**3389**|TCP|**RDP**|Remote Desktop. Target for **BlueKeep**, brute-forcing, or password spraying.|

### 🌐 Web & Name Services

|Port|Proto|Service|PNPT/Pentest Context|
|---|---|---|---|
|**53**|TCP/UDP|**DNS**|UDP = Queries, TCP = **Zone Transfers**. Look for internal IP leaks.|
|**80**|TCP|**HTTP**|Unencrypted web. Traffic can be sniffed.|
|**443**|TCP|**HTTPS**|Encrypted web. Check SSL certificates for domain info.|

### 📧 Email

|Port|Proto|Service|PNPT/Pentest Context|
|---|---|---|---|
|**25**|TCP|**SMTP**|Sending mail. Check for **VRFY/EXPN** commands to enumerate users.|
|**110**|TCP|**POP3**|Receiving mail (downloads to device).|
|**143**|TCP|**IMAP**|Receiving mail (stored on server).|

### 🗄️ Database & Directory Services

|Port|Proto|Service|PNPT/Pentest Context|
|---|---|---|---|
|**161**|UDP|**SNMP**|Network Mgmt. Look for default community strings (`public`/`private`) to map networks.|
|**389**|TCP/UDP|**LDAP**|Directory Access. Critical for **Active Directory** enumeration.|
|**445**|TCP|**SMB**|Windows File Shares. **Critical Target** (Enumeration, EternalBlue, PSExec).|
|**3306**|TCP|**MySQL**|Database. Try default creds (`root`:``) or SQL injection vectors.|

### ⚙️ Network Config

|Port|Proto|Service|Description|
|---|---|---|---|
|**67/68**|UDP|**DHCP**|Assigns IP addresses.|
|**123**|UDP|**NTP**|Time synchronization.|

---

### ❓ Question: Does "External Blue" use SMB?

**Yes.**

- **Exploit Name:** EternalBlue (MS17-010).
- **Target Port:** **445 (SMBv1)**.
- **Significance:** It is a critical remote code execution (RCE) vulnerability in the Microsoft Server Message Block (SMB) protocol. It allows an attacker to compromise a target without any authentication.
- **PNPT Note:** Always scan port 445 carefully. Even if EternalBlue is patched, 445 is used to enumerate user lists, shares, and is the primary vector for moving laterally in an Active Directory environment.