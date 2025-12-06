

**Concept:** The Internet Protocol (IP) provides identification and location for devices on a network.
**OSI Layer:** Layer 3 (Network Layer).
**Primary Device:** Routers (route traffic based on IP addresses).

### IPv4 vs. IPv6 Comparison

| Feature | IPv4 | IPv6 |
| :--- | :--- | :--- |
| **Address Length** | 32-bit | 128-bit |
| **Format** | Dotted-Decimal | Hexadecimal |
| **Structure** | 4 Octets (8-bit sections) | 8 Groups (16-bit sections) |
| **Separator** | Period (`.`) | Colon (`:`) |
| **Address Space** | ~4.3 Billion (Depleted) | ~3.4 x 10^38 (Virtually Unlimited) |
| **Compatibility** | Legacy standard | Modern standard (Security/Auto-config built-in) |

### IPv6 Notation Rules
IPv6 addresses are long, so they use shorthand rules:
1.  **Omit Leading Zeros:** `0db8` becomes `db8`.
2.  **Zero Compression:** Consecutive groups of zeros can be replaced by a double colon (`::`).
    *   *Note:* `::` can only be used **once** per address.
    *   *Example:* `2001:0db8:0000:0000:0000:0000:1428:57ab` $\rightarrow$ `2001:db8::1428:57ab`

### Private IP Addresses (IPv4)
Addresses reserved for private LANs. They are **not** routable on the public internet.

*   **Class A:** `10.0.0.0` to `10.255.255.255` (Large networks)
*   **Class B:** `172.16.0.0` to `172.31.255.255`
*   **Class C:** `192.168.0.0` to `192.168.255.255` (Home/Small business)

> **Key Takeaway:** If you see `192.168.x.x` during an assessment, you are looking at an internal network address, not a public-facing server.

### Practical Identification (Linux CLI)
When running `ifconfig` or `ip addr`:
*   **`inet`**: Denotes the IPv4 address.
*   **`inet6`**: Denotes the IPv6 address.