**Definition:** A conceptual framework standardizing communication functions into seven distinct layers.  
**Key Benefit:** Modular approach facilitates troubleshooting, interoperability, and design.

## The 7 Layers (Bottom-Up)

A common mnemonic to remember the layers (Layer 1 to 7):

> **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way  
> (Physical, Data Link, Network, Transport, Session, Presentation, Application)

| Layer # | Layer Name       | Function                                                              | PDU (Unit)  | Key Protocols/Examples                    |
| ------- | ---------------- | --------------------------------------------------------------------- | ----------- | ----------------------------------------- |
| **7**   | **Application**  | End-user interaction; network services to applications.               | Data        | HTTP, FTP, SMTP, DNS, SSH                 |
| **6**   | **Presentation** | Data representation, encryption (SSL/TLS), and formatting.            | Data        | JPEG, ASCII, GIF, SSL/TLS                 |
| **5**   | **Session**      | Establishes, manages, and terminates connections between apps.        | Data        | APIs, NetBIOS, RPC                        |
| **4**   | **Transport**    | Reliable delivery, flow control, segmentation, and error recovery.    | **Segment** | **TCP** (Reliable), **UDP** (Fast), Ports |
| **3**   | **Network**      | Logical addressing (IP) and path selection (Routing).                 | **Packet**  | **IPv4**, IPv6, ICMP, IPSec, Routers      |
| **2**   | **Data Link**    | Physical addressing (MAC), error detection, framing.                  | **Frame**   | Ethernet, Wi-Fi (802.11), Switches, ARP   |
| **1**   | **Physical**     | Transmission of raw bits over physical medium (electric/light/radio). | **Bit**     | Cables (Cat6, Fiber), Hubs, Repeaters     |

## Key Concepts for Pentesting

- **Encapsulation:** As data moves down the stack (Layer 7 →→ 1), headers are added.
- **De-encapsulation:** As data moves up the stack (Layer 1 →→ 7), headers are stripped.
- **TCP vs. UDP (Layer 4):**
    - **TCP:** Connection-oriented (3-way handshake), reliable, slower. (e.g., Web browsing, Email).
    - **UDP:** Connection-less, "fire and forget," faster, unreliable. (e.g., Streaming, VoIP, DNS).

## Why this matters for PNPT:

1. **Layer 2 Attacks:** ARP Spoofing, MAC Flooding, VLAN Hopping occur here.
2. **Layer 3 Attacks:** Ping sweeps, IP Spoofing, Routing attacks.
3. **Layer 4 Attacks:** Port Scanning (Nmap), SYN Floods.
4. **Layer 7 Attacks:** Web App attacks (SQLi, XSS), Phishing.
5. **Troubleshooting:** Understanding where a connection