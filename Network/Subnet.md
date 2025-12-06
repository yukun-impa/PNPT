
## 1. Core Concepts

**Subnetting** is the process of dividing a single large network into smaller, manageable logical subnetworks (subnets).

- **Purpose:** improving network efficiency, reducing broadcast traffic, and facilitating management/security segregation.
- **Mechanism:** "Borrowing" bits from the **Host** portion of the IP address to create additional **Network** identifiers.

## 2. CIDR Notation

**CIDR (Classless Inter-Domain Routing)** is the standard syntax for referencing IP networks.

- **Format:** `IP_Address / Prefix_Length`
- **Prefix Length:** The number of bits (counting from left to right) set to `1` that represent the **Network**. The remaining bits are for **Hosts**.

### Example: `/24` Network

**IP:** `192.168.0.0/24`

- **Binary:** `11111111.11111111.11111111.00000000`
- **Subnet Mask:** `255.255.255.0`
- **Breakdown:**
    - First 24 bits = Network (Fixed)
    - Last 8 bits = Host (Variable)

---

## 3. Subnetting Implementation (Borrowing Bits)

To create subnets, you move the prefix length to the right (borrow bits from the host).

### Scenario: Subnetting a `/24` to `/26`

We borrow **2 bits** from the host portion to create subnets.

1. **Old Mask:** `/24`
2. **New Mask:** `/26` (`/24` + 2 borrowed bits)
3. **New Subnet Mask:** `255.255.255.192` (Binary ending in `11000000`)

### The Math

- **Number of Subnets created:** 2�2n (where �n is bits borrowed).
    - 22=422=4 Subnets.
- **Block Size (Total IPs per subnet):** 2ℎ2h (where ℎh is remaining host bits).
    - 32 total bits - 26 network bits = 6 host bits.
    - 26=6426=64 IPs per subnet.

### Resulting Networks

|Subnet|Network Address (ID)|Range|Broadcast Address|
|---|---|---|---|
|**1**|`192.168.0.0`|`.0` - `.63`|`192.168.0.63`|
|**2**|`192.168.0.64`|`.64` - `.127`|`192.168.0.127`|
|**3**|`192.168.0.128`|`.128` - `.191`|`192.168.0.191`|
|**4**|`192.168.0.192`|`.192` - `.255`|`192.168.0.255`|

> **Pentester Note:** When scanning a subnet (e.g., with Nmap), remember:
> 
> - **First IP:** Network ID (Unusable for hosts)
> - **Last IP:** Broadcast Address (Unusable for hosts)
> - **Usable Hosts:** Total IPs - 2.

---

## 4. Quick Reference Cheat Sheet

|CIDR|Subnet Mask|Total IPs|Usable Hosts|Common Use|
|---|---|---|---|---|
|**/8**|`255.0.0.0`|16,777,216|16M+|Large Corps / ISP|
|**/16**|`255.255.0.0`|65,536|65,534|Medium Business|
|**/24**|`255.255.255.0`|256|254|Home / Small Office|
|**/29**|`255.255.255.248`||||

Deeply thought

(0.0s)

8 | 6 | Point-to-Point Links |  
| **/32** | `255.255.255.255` | 1 | 1 | Single Host (Statics) |