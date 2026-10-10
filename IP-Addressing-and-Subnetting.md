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

Note: Modern IPv4 networking uses CIDR rather than class-based addressing.
