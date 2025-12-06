
## 1. Core Concepts
*   **Definition:** A unique, physical identifier assigned to a Network Interface Controller (NIC).
*   **Type:** Hardware address (burned into firmware/ROM).
*   **OSI Layer:** **Layer 2 (Data Link Layer)**.
*   **Purpose:** Ensures data delivery to the correct device within a specifically **Local Area Network (LAN)**.

## 2. Structure
*   **Length:** 48 bits (6 bytes).
*   **Format:** Hexadecimal pairs separated by colons (e.g., `00:1A:2B:3C:4D:5E`).
*   **Composition:**
    *   **First 3 Bytes (24 bits):** Organizationally Unique Identifier (**OUI**). Identifies the manufacturer (e.g., Dell, Cisco, Apple).
    *   **Last 3 Bytes (24 bits):** Network Interface Controller Specific. Like a serial number for that specific card.

## 3. Networking Logic
*   **Scope:** Local network segment only. MAC addresses do **not** route across the internet.
*   **Encapsulation:** Data is wrapped in **Ethernet Frames** containing Source and Destination MACs.
*   **Switching:** Switches use MAC address tables to forward packets to the specific port where the destination MAC resides.

## 4. MAC vs. IP
| Feature         | MAC Address          | IP Address           |
| :-------------- | :------------------- | :------------------- |
| **Layer**       | Layer 2 (Data Link)  | Layer 3 (Network)    |
| **Type**        | Physical / Permanent | Logical / Temporary  |
| **Scope**       | Local Network (LAN)  | Global / Internet    |
| **Assignation** | Manufacturer         | Network Admin / DHCP |
