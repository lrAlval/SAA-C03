![[Pasted image 20221101210003.png]]
# VPC Virtual Private Cloud

## TLDR
A stack of AWS resources, more clearly the connectivity and setup options for and between these resources.

## Facts
- **Max** 5 VPCs per region 
	- soft limit
- AWS reserves **5** IP addresses (first 4 & last 1) in each **subnet**.
![[Pasted image 20230712231714.png]]
- Max **CIDR** per VPC is 5 for **each** CIDR:
	- Min size is /28 (16 IP addresses)
	- Max size /16 (65 536 IP address)
- Because **VPC** is **private**, **only** the private IPv4 ranges are allowed:
	- 10.0.0.0 – 10.255.255.255 (10.0.0.0/8)
	- 172.16.0.0 – 172.31.255.255 (172.16.0.0/12)
	- 192.168.0.0 – 192.168.255.255 (192.168.0.0/16)

## VPN Limitations

- supports only **IPSec** tunnel mode. Transport mode is currently not supported.
- supports only one VGW can be attached to a VPC at a time.
- does not support IPv6 traffic on a virtual private gateway.
- does not support Path MTU Discovery.
- does not support overlapping CIDR blocks for the networks. It is recommended to use non-overlapping CIDR blocks.
- does not support **transitive routing**.
- So for traffic from **on-premises** to **AWS** via a **Virtual Private Gateway(VGW)**, it
    - Does not support **Internet** connectivity through **Internet Gateway**.
    - Does not support Internet connectivity through [NAT Gateway](https://jayendrapatil.com/aws-vpc-nat/)
    - Does not support VPC Peered resources access through [VPC Peering](https://jayendrapatil.com/aws-vpc-peering/)
    - Does not support **S3**, **DynamoDB** access through [VPC Gateway Endpoint](https://jayendrapatil.com/aws-vpc-endpoints/)
    - However, Internet connectivity through **NAT instance** and **VPC Interface Endpoint** or **PrivateLink** services are accessible.
- Provides a bandwidth of 1.25 Gbps, currently.

## VPC Considerations

- What size should the VPC be. This will limit the use.
- Define how many AZs are required (**subnets**) early.
-   Are there any networks we can't use?.
-   Be mindful of ranges other **VPCs** use or are used in other cloud environments.
-   Try to predict the future uses.
	- Always aim for at least an **extra** **network** ranges.
-   VPC structure with tiers and resilience (availability) zones
-   VPC min /**28** network (**16** IP)
-   VPC max /**16** (65456 IP)
-  172.16.0.0/12 default VPC
-   Avoid common range **10.0** or **10.1**, include up to **10**.**10**
    -   Suggest starting of **10.16** for a nice clean base 2 number.
    
![[Pasted image 20230706222922.png]]

https://www.ipaddressguide.com/cidr

Reserve 2+ network ranges per region being used per account. Think of the highest region you will operate in and add extra as a buffer.

An example using 4 AWS accounts.

-   Regions with 2 ranges in each Region
    -   3 regions in US
    -   1 region in Europe
    -   1 region in AUS
-   Total of 40 ranges, 10 ranges for each account.

| VPC Size    | Netmask | Subnet Size | Hosts/Subnet* | Subnet/VPC | Total IPs |
| ----------- | ------- | ----------- | ------------- | ---------- | --------- |
| Micro       | /24     | /27         | 27            | 8          | 216       |
| Small       | /21     | /24         | 251           | 8          | 2008      |
| Medium      | /19     | /22         | 1019          | 8          | 8152      |
| Large       | /18     | /21         | 2043          | 8          | 16344     |
| Extra Large | /16     | /20         | 4091          | 16         | 65456     |


### Custom VPC

-   **Regional**, Isolated and Resilient Service.
    -   Operates from all **AZ's** in that region
-   allows **isolated** networks inside AWS.
-   Nothing **IN** or **OUT** of a VPC without **explicit** configuration.
    -   Isolated blast radius. 
    - Any problems are limited to that **VPC** or anything connected to it.
-   Flexible configuration
-   Hybrid networking to allow connection to other cloud or on-premise networking.
-   Default or Dedicated Tenancy. 
	- This refers to how the hardware is configured.
	-  Default allows on a per resource **decision** later on.
	-  Dedicated locks any **resourced** created in that VPC to be on dedicated hardware, which comes at a cost premium.
## Gateways
### Internet Gateway (IGW)
- allows resources (EC2) in a VPC to connect to the internet.
- Allows all IPs **IN** and **OUT**.
- Scales **horizontally** and is **highly** available and redundant.
- Must be created separately from a VPC
- one VPC can only be attached to **one** **IGW** and vice versa.
- **IGW** on their own do not allow internet access.

# Egress-only internet gateway
- **outbound traffic** **IPv6** only
- allows **outbound-only** (from inside the instances to the internet)
- **prevents** the Internet from initiating an IPv6 connection.

### NAT Gateway
- old way (**NAT instance**-deprecated)
- AWS managed, higher bandwidth, **HA**, no administration.
- Pay **per** hour for **usage** and bandwidth.
- Fixed to a **single** **AZ**, uses **Elastic IP**
	- Must create multiple **NAT** **Gateways** in **multiple AZs** for [[Resilience concepts#^6c176e|FT]]
	- no cross-AZ **failover** needed because if an **AZ** goes down it doesn't need **NAT**.
- can't be used by EC2 instance in same **subnet** (only from other **subnets**)
- Requires an **IGW** (Private subnet => **NATGW** => **IGW**)
- No Security Groups to manage / **required**.

![[Pasted image 20231016183609.png]]
**TL;DR:**
- Internet Gateway (**IGW**) allows instances with **public IPs** to access the internet.
- NAT Gateway (**NGW**) allows instances with **no public IPs** to access the internet.

## AWS Site-to-Site **VPN** 

### Virtual Private Gate (VPGW)
- VPN concentrator on the AWS side of the VPN connection
- VGW is created and attached to VPC from which you want to create the Site-Site VPN Connection
- Possibility to customize the ASN (Autonomous System Number)

### Customer Gateway (CGW)
- software app or physical device on customer side of the VPN connection 
- if customer gate is behind public ip , use public ip
- if is behind private IP, use the public IP of the NAT device that's enabled for traversal (NAT-T)
- enable **route propagation** for **VGW** in the route table that is associated with your **subnets**
- if you need to ping your EC2 instances from on-premises.
	- Enable ICMP protocol on the inbound of your [[SecurityGroup]]
## VPN CloudHub
- low-cost **hub-and-spoke** model for primary or secondary network connectivity between different locations (VPN only)
- it's a VPN connection, so it goes over the public internet.
- Connect multiple VPN connections on the same VPGW
	- set up dynamic routing
	- configure route tables.
### Options

#### VPC with public subnet
- single public subnet
- internet gateway
- recommended for simple public facing application

#### VPC with public and private subnets
- public subnet
- private subnet
- internet gateway
- recommended for 2 tier application

#### VPC with public, private subnets and AWS Site-to-Site [[VPN]]
- public subnet
- private subnet
- virtual private gatway
- internet gateway
- recommended to extend network into the cloud and some ressource are internet facing

#### VPC with private subnet and AWS Site-to-Site [[VPN]]
- private subnet
- virtual private gateway
- recommended to extend private network into the cloud

## VPC Endpoint
- Privately **connect** a **VPC** to supported services 
- does not require an internet gateway, [[NAT]], [[VPN]] or [[DirectConnect (DX)]]
- instances don't require public IP addresses.
- Uses AWS Private Link as connection Line.
- Data does not leave **AWS** while communicating.
- Doesn't support **inter-region** communication.

### Interface Endpoint (powered by PrivateLink)
- ENI with private IP **address** in the target subnet
- supports most AWS **services**
- Recommended  for 
	- **on-premises** (Site to SiteVPN or [[DirectConnect (DX)]])
	- different VPC
	- different region
- $ per hour + $ per GB of data **processed**.

![[Pasted image 20231017170844.png]]
### Gateway Endpoint
- Generally recommended for most **use cases**.
- only for [[S3]] and [[DynamoDB]]
- gateway **which** you set as a route target 
- **Free** 
![[Pasted image 20231018173628.png]]
## VPC Peering
- Connection between 2 **VPCs** using private addresses
- works **cross-regions**
- not transitive
- need to setup **route** **tables**

### Transit Gateway
- **hub** for multiple peering connections
- regional resource but can work cross-region
- share cross-account using resource access manager (RAM)
- peer transit gateways across regions.
- only service supports that **IP-Multicast**
- route tables
	- limit which VPC can talk to other VPC
- Attach options are, 
	- **VPC**
	- direct connect gateway or 
	- another transit gateway either as peering or **VPN**.
- MTU = max package size
- MTU 85kbs if direct connect or peering **VPC**
- MTU 15kbs if [[VPN]]
- has a route table
- route propagation
- gives double throughput of virtual private gateway by using ECMP support.
- 
![[Pasted image 20231018182425.png]]
## Use cases
### Transit gateway site to site vpn ecmp
- increase the bandwidth and performance of on premise to multiple vpns

![[Pasted image 20231018182940.png]]

### Share Direct Connect between multiple accounts

![[Pasted image 20231018183129.png]]
## VPC Sharing
- share one or more subnets within other accounts beloning to the same [[AWS Organizations]]
- every account can only work with the ressources they created

## VPC Flow Logs
- Capture Information about IP traffic through your interfaces
- VPC Flow Logs
- Subnet Flow Logs
- ENI Flow Logs
![[Pasted image 20231018174459.png]]
### Other Sources
- [[ELB]]
- [[RDS]]
- [[ElastiCache]]
- [[Amazon Redshift]]
- WorkSpaces 
- **NATGW**
- Transit Gateway
...


### Targets
- [[S3]]
- [[CloudWatch]] Logs
### Information
- ip information
- port information
- action (accept/reject)

### Query
- [[S3]] Athena
- [[CloudWatch]] Logs Insights

## Network Access Control List (NACL)
- not **stateful* *
- **Stateless**
- one per **subnet**
	- new subnets have default **NACL**
- rules have a **number** (1-32766) that define which rules take precedence over the other (first match wins)
	- the **lower the number**, higher precedence
	- 100 ALLOW 10.0.0.10/32
	- 200 DENY 10.0.0.10/32
	- last rule is an asterisk * → denies a request in case no rule match
	- the IP address will be allowed because **100** has a higher precedence over **200**.
- New created NACLS will deny everything by default.
- **Firewall** on **subnet** level
	- required to defined inbound and outbound rules **explicitly** .
- For **outbound** traffic allow **ephemeral** ports **32768**-**65535** (all ports for different services to listen for outbound traffic)
- Ephemeral port:
	- Windows: 49152 - 65535
	- Linux: 32768 - 60999
- Default NACLS assigned to subnets **allow** all by default.
  ![[Pasted image 20231017162432.png]]

Security Group vs NACLs - Differences:
![[Pasted image 20231017163239.png]]
## VPC Traffic Mirroring
- capture and inspect network traffic
- unintrusive
- traffic gets direct to security applicance fleet
- fleet redicet traffic back