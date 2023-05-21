####  IPv4 - RFC 791 (1981)

Dotted decimal notation for human readability.

-   4 numbers from 0 to 255 separated by a period.
-   Octet are the numbers between the period.
- Manually assigned or by a **DHCP server**
-  the Network **Prefixes or network mask or also know as subnet mask purpose** is to allow devices to **identify and route** data packets between different networks using IP addresses.
    -   additionally you can identify how many networks can a subnet mask have by taking into account the following:
    -   ****IPv4 we can only use **32bits** prefixes, ipv6 can go up to **128 bits.**
    -   0 (**lowest**) means 0 for the network and 0 for the host
    -   **16 for the network, 16 for the host so the network can have (65.536) IP addresses**
    -   **24** the first 24 bits are for the network and **8** for the host. so the host network can have (**256** IP addresses - 2 = 254)
    -   **32** (highest) for the network and 0 for the host , so the network can have **1** **IP addresses**
    -   Formula : e.g. in a subnet /24 we could have **2^8** (8 bits for the host) - 2 = **254**

There are just over 4 billion addresses. This was not very flexible because it was either too small or large for some corporations. Some IP addresses was always left unused.

#### Classful Addressing

-   Class A range
    -   Starts at `0.0.0.0` and ends at `127.255.255.255`.
    -   Split into 128 class A networks
    -   Handed out to large companies
-   Class B Range
    -   Half the range of class A.
    -   Starts at `128.0.0.0` and ends at `191.255.255.255`.
-   Class C Range
    -   Half of range class B
    -   Starts at `192.0.0.0` and ends at `223.255.255.255`.

####  Internet / Private IPs - RFC1918

These can't communicate over the internet and are used internally only

-   One class A network: `10.0.0.0` - `10.255.255.255`
-   16 Class B networks: `172.16.0.0` - `172.31.255.255`
-   256 Class C networks: `192.168.0.0` - `192.168.255.255`

####  Classless inter-domain routing (CIDR)

CIDR networks are represented by the starting IP address of the network called the network address and the prefix.

CIDR Example: `10.0.0.0/16`

-   `10.0.0.0` is the first address on the network
-   /16 is the size of the network called the prefix.
    -   The bigger the prefix, the smaller the network
    -   The smaller the prefix, the bigger the network.
-   /16 provides 65,536 addresses.
-   `10.0.0.0/17` and `10.0.128.0/17` are each half of the original example.
    -   This is called **subnetting**

#### IP address notations to remember

-   `0.0.0.0/0` means all IP addresses
-   `10.0.0.0/8` means 10.ANYTHING - Class A
-   `10.0.0.0/16` means 10.0.ANYTHING - Class B
-   `10.0.0.0/24` means 10.0.0.ANYTHING - Class C
-   `10.0.0.0/32` means only 1 IP address

`10.0.0.0/16` is the equivalent of `1234` as a password. You should consider other ranges that people might use to ensure it does not overlap.

#### Packets

Contains:

-   source IP address
-   destination IP address
-   data the source IP wants to communicate with the destination IP.

TCP and UDP are protocols built on top of IP.

-   TCPIP means TCP running with IP
-   UDPIP means UDP running with IP

TCP/UDP Segment has a source and destination port number. This allows devices to have multiple conversations at the same time. In AWS when data goes through network devices, filters can be set based on IP addresses and port numbers.

#### IPv6 - RFC 8200 (2017)

`2001:0db8:28ac:0000:0000:82ae:3910:7334`

The value is hex and there are two octets per spacing or one hextet. The redundant zeros can be removed to create:

`2001:0db8:28ac:0:0:82ae:3910:7334`

or you can remove them all entirely once per address

`2001:0db8:28ac::82ae:3910:7334`

Each address is 128 bits long. They are addressed by the start of the network and the prefix. Since each grouping is 16 values, we can multiple the groups by this to achieve the prefix.

`2001:0db8:28ac::/48` really means the network starts at `2001:0db8:28ac:0000:0000:0000:0000:0000` and finishes at `2001:0db8:28ac:ffff:ffff:ffff:ffff:ffff`

`::/0` represents all IPv6 addresses