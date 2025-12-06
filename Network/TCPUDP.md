## TCP vs. UDP

|Feature|TCP (Transmission Control Protocol)|UDP (User Datagram Protocol)|
|---|---|---|
|**Type**|Connection-Oriented|Connectionless|
|**Reliability**|**High:** Guaranteed delivery, error-checking, sequencing.|**Low:** "Fire and forget." No delivery guarantee.|
|**Speed**|Slower (due to overhead).|Faster (low overhead).|
|**Flow Control**|Yes (Acknowledgements/Retransmission).|No.|
|**Use Cases**|HTTP/S, SSH, FTP, SMTP (Needs accuracy).|DNS, VoIP, Streaming, SNMP (Needs speed).|

## TCP 3-Way Handshake

Before data transfers via TCP, a connection must be established. This is critical for understanding how **Nmap** scans work.

1. **SYN (Synchronize)**
    - **Sender:** Client (Attacker)
    - **Action:** Sends packet with `SYN` flag.
    - **Meaning:** "I want to open a connection."
2. **SYN-ACK (Synchronize-Acknowledge)**
    - **Sender:** Server (Target)
    - **Action:** Responds with `SYN` and `ACK` flags.
    - **Meaning:** "I received your request, and I am open to connect."
3. **ACK (Acknowledge)**
    - **Sender:** Client (Attacker)
    - **Action:** Sends packet with `ACK` flag.
    - **Meaning:** "Connection established." (Data transfer begins).

> **Visual:** `Client (SYN) -> Server (SYN-ACK) -> Client (ACK)`

---

## 🛡️ Pentester's Perspective (Scanning)

Understanding the protocol dictates how we interpret scan results (e.g., Nmap).

### Scanning TCP

- **Method:** We usually manipulate the handshake (e.g., SYN Scan / Stealth Scan `-sS`).
- **Response Logic:**
    - If we send `SYN` and get `SYN-ACK` →→ **Port is OPEN**.
    - If we send `SYN` and get `RST` (Reset) →→ **Port is CLOSED**.
    - If we send `SYN` and get no response/ICMP error →→ **FILTERED** (Firewall).

### Scanning UDP

- **Difficulty:** Significantly slower and less reliable than TCP scanning.
- **Method:** Nmap (`-sU`).
- **Response Logic:**
    - If we send data and get a UDP response →→ **Port is OPEN**.
    - If we send data and get **ICMP Port Unreachable** →→ **Port is CLOSED**.
    - If we send data and get **No Response** →→ **OPEN|FILTERED**.
- **Note:** Because UDP doesn't send ACKs, we often cannot distinguish between an empty port and a firewalled port without further probing.