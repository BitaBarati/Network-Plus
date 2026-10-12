# Network+ — IP Addressing and Subnetting
## 1. IP Address Fundamentals
- **IP Address**: Logical address used to identify a network interface at the Network Layer.
- **IPv4**: 32-bit address, written as four decimal octets (e.g., 192.168.1.10).
- **IPv6**: 128-bit address, written in hexadecimal notation.
- **MAC Address**: Link-layer address used for communication within a local network.
- **Network ID**: Identifies the network portion of an IP address.
- **Host ID**: Identifies a host within a subnet.
- **Subnet Mask**: Identifies network and host portions in IPv4.
- **CIDR (Classless Inter-Domain Routing)**: Represents a network prefix, e.g., 192.168.1.0/24.
- **Prefix Length**: Number of network bits in an address.

### IPv4 Address Types
- **Public IP**: Globally routable address.
- **Private IP**: Used within private networks; not globally routable.
- **Static IP**: Manually configured or persistently assigned address.
- **Dynamic IP**: Automatically assigned, commonly through DHCP.
- **Loopback**: 127.0.0.1 (IPv4), ::1 (IPv6).
- **APIPA / IPv4 Link-Local**: 169.254.0.0/16; commonly assigned when DHCP configuration fails.

### Private IPv4 Ranges (RFC 1918)

| CIDR | Address Range |
|:---|:---:|
|10.0.0.0/8|10.0.0.0 – 10.255.255.255|
|172.16.0.0/12|172.16.0.0 – 172.31.255.255|
|192.168.0.0/16|192.168.0.0 – 192.168.255.255|

## 2. IPv4 Classes (Historical)

|Class|First Octet|Default Prefix|
|:---|:---:|:---|
|A|1–126*|/8|
|B|128–191|/16|
|C|192–223|/24|
|D|224–239|Multicast|
|E|240–255|Reserved / experimental|

* 127.0.0.0/8 is reserved for loopback.

**Note:** Modern IPv4 networking uses CIDR rather than class-based addressing.

## 3. Address Allocation and Network Services

- ** ICANN: Coordinates policies related to the global Internet’s unique identifiers.
- ** IANA: Coordinates global IP address and protocol-parameter registries and allocations.
- ** RIR (Regional Internet Registry): Manages IP address resources for a geographic region.
- ** RIPE NCC: RIR serving Europe, the Middle East, and parts of Central Asia.
- ** LIR (Local Internet Registry): Organization that receives and distributes IP resources under an RIR.
- ** NAT (Network Address Translation): Translates IP addresses between network realms.
- ** DHCP: Automatically provides IP configuration to clients.
- ** DHCP Reservation: Assigns a predictable IP address to a client based on an identifier, commonly its MAC address.

### DHCP DORA Process

 1. **Discover**
 2. **Offer**
 3. **Request**
 4. **Acknowledge**

### Local Name Resolution and Service Discovery

- **mDNS: Multicast DNS for local name resolution without conventional DNS infrastructure.
- **DNS-SD: Discovers services using DNS records.
- **LLMNR: Link-Local Multicast Name Resolution; a legacy local name-resolution mechanism.

### Zero-Configuration Networking

Techniques that enable devices to communicate with minimal manual configuration, including link-local addressing, mDNS, and DNS-SD.

## 4. Subnetting and Supernetting

- **Subnetting:** Divides a network into smaller networks by borrowing host bits.
- **Supernetting:** Combines contiguous address blocks into a larger CIDR block.
- **Route Summarization:** Advertises multiple routes as a shorter prefix when the routes can be safely aggregated.
- **CIDR Block:** Address range represented by a prefix.
- **IP Calculator:** Tool for calculating network address, broadcast address, subnet mask, and usable host range.

### Useful Formulas

For a conventional IPv4 subnet with (h) host bits:

- **Total addresses:** (2^h)
- **Usable host addresses:** (2^h - 2)
- **Number of equal subnets created by borrowing (s) bits:** (2^s)

**Note:** The usable-host formula has exceptions for special prefixes such as /31 and /32.

### Subnet Mask Reference

| CIDR | Subnet Mask | Total IPs | Usable Hosts* |
|---|---|---:|---:|
| `/24` | `255.255.255.0` | 256 | 254 |
| `/25` | `255.255.255.128` | 128 | 126 |
| `/26` | `255.255.255.192` | 64 | 62 |
| `/27` | `255.255.255.224` | 32 | 30 |
| `/28` | `255.255.255.240` | 16 | 14 |
| `/29` | `255.255.255.248` | 8 | 6 |
| `/30` | `255.255.255.252` | 4 | 2 

\* Conventional IPv4 subnets.

## 5. Route Summarization Examples

### Example 1: Four /24 Networks

**Original Networks**

'''text
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
----------------
192.168.0.0/22

### Example 2: Sixteen /24 Networks

172.16.0.0/24
...
172.31.0.0/24
----------------
172.16.0.0/20

**Correction:** The aggregate is /20, not /12. 172.16.0.0/12 represents the entire private range from 172.16.0.0 through 172.31.255.255.

** 6. Subnetting Exercises

*** Exercise 1: Divide 192.168.1.0/24 into 4 Equal Subnets

- **Borrow 2 bits:** (2^2 = 4)
- ** New prefix:** /26
- **Subnet mask:** 255.255.255.192
- **Usable hosts per subnet:** 62


| Network | Usable Host Range | Broadcast |
|---|---|---|
| `192.168.1.0/26` | `192.168.1.1 – 192.168.1.62` | `192.168.1.63` |
| `192.168.1.64/26` | `192.168.1.65 – 192.168.1.126` | `192.168.1.127` |
| `192.168.1.128/26` | `192.168.1.129 – 192.168.1.190` | `192.168.1.191` |
| `192.168.1.192/26` | `192.168.1.193 – 192.168.1.254` | `192.168.1.255` |


### Exercise 2: Divide 192.168.1.0/24 into 4 Subnets, Each Supporting at Least 30 Hosts

**Requirements and Calculation**

- **Required usable hosts:** 30 per subnet
- **Prefix:** /27
- **Subnet mask:** 255.255.255.224
- **Total addresses per subnet:** 32
- **Usable hosts per subnet:** 30




| Network | Usable Host Range | Broadcast |
|---|---|---|
| `192.168.1.0/27` | `192.168.1.1 – 192.168.1.30` | `192.168.1.31` |
| `192.168.1.32/27` | `192.168.1.33 – 192.168.1.62` | `192.168.1.63` |
| `192.168.1.64/27` | `192.168.1.65 – 192.168.1.94` | `192.168.1.95` |
| `192.168.1.96/27` | `192.168.1.97 – 192.168.1.126` | `192.168.1.127'|

### Exercise 3: Divide 192.168.80.0/24 into 2 Equal Subnets

- **Borrow 1 bit:** (2^1 = 2)
- **New prefix:** /25
- **Subnet mask:** 255.255.255.128
- **Usable hosts per subnet:** 126



| Network | Usable Host Range | Broadcast |
|---|---|---|
| `192.168.80.0/25` | `192.168.80.1 – 192.168.80.126` | `192.168.80.127` |
| `192.168.80.128/25` | `192.168.80.129 – 192.168.80.254` | `192.168.80.255`|


### Exercise 4: Create 2 Subnets Supporting 8,000 Hosts Each from 10.0.0.0/8

- **Required usable hosts per subnet:** 8,000
- **Host bits required:** 13
- **Prefix:** /19
- **Subnet mask:** 255.255.224.0
- **Total addresses per subnet:** 8,192
- **Usable hosts per subnet:** 8,190


 
| Network | Usable Host Range | Broadcast |
|---|---|---|
| `10.0.0.0/19` | `10.0.0.1 – 10.0.31.254` | `10.0.31.255` |
| `10.0.32.0/19` | `10.0.32.1 – 10.0.63.254` | `10.0.63.255`|


## 7. VLSM (Variable Length Subnet Mask)

VLSM allows subnets of different sizes within the same address block. Allocate the largest subnet first.

### Example: Allocate Subnets for 100, 50, and 20 Hosts

Requirement: Create subnets supporting 100, 50, and 20 usable hosts from 192.168.1.0/24.

| Required Hosts | Prefix | Network | Usable Host Range | Broadcast |
|---:|---|---|---|---|
| 100 | `/25` | `192.168.1.0` | `192.168.1.1 – 192.168.1.126` | `192.168.1.127` |
| 50 | `/26` | `192.168.1.128` | `192.168.1.129 – 192.168.1.190` | `192.168.1.191` |
| 20 | `/27` | `192.168.1.192` | `192.168.1.193 – 192.168.1.222` | `192.168.1.223`|


**Remaining unallocated range:** 192.168.1.224/27

## 8. Useful References

- **IANA — IPv4 Special-Purpose Address Registry⁠￼
- **RFC 1918 — Private IPv4 Addressing⁠￼
- **RFC 4632 — CIDR and Route Aggregation⁠￼

# 9. Tools

- **NirSoft⁠￼ — Windows network and system utilities.
- **IP Calculator — Use any trusted subnet calculator to verify subnetting results.