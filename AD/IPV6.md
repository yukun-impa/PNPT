## Overview

Another form of relay/spoofing attack that abuses DNS via IPv6.

**Key Concept:** Windows queries for IPv6 addresses even in IPv4-only environments.

## Attack Tool

BASH

`1mitm6 -d <domain> 2ntlmrelayx.py -6 -t ldaps://<DC_IP> -wh fakewpad.<domain> -l lootme 3`

## When It Happens

- Attacker sets up rogue DHCPv6 server
- Windows machines request IPv6 configuration
- Attacker responds, becoming the DNS server
- Victim traffic gets redirected → credentials relayed

## Mitigation Strategies

### 1. Disable IPv6 via Firewall (if not needed)

Block these Windows Firewall rules:

|Direction|Rule|
|---|---|
|Inbound|Core Networking - DHCPv6 (DHCPV6-In)|
|Inbound|Core Networking - Router Advertisement (ICMPv6-In)|
|Outbound|Core Networking - DHCPv6 (DHCPV6-Out)|

### 2. Disable WPAD

If WPAD is not used, disable it via GPO.

### 3. Enable LDAP Protections

LDAP/LDAPS relay can **only** be mitigated by enabling **both**:

- LDAP Signing
- LDAP Channel Binding

### 4. Protect Privileged Accounts

- Add admin users to **Protected Users** group
- Or mark accounts as **"Account is sensitive and cannot be delegated"**