![[Pasted image 20221031111307.png]]
# VPN

## TLDR
Access **AWS** Resources in one or more  [[docs/networks/VPC]]s as if they **were** in your on premise network.

## Design
- Use non overlapping IP ranges for **each** network.
- Use **Transit Gateway** to increase throughput for a single site, this allows multipath routing using additional **VPN** Tunnel lds.

## Options

### AWS Managed VPN
- **over** internet
- AWS managed
- use this to take advantage of AWS managed services for failover and redundancy
- one Virtual Private gateway to multiple Customer Gateways

#### Pro
- reuses existing VPN equipment.
- Reuses existing internet connection.
- Highly available.
- Static routes, Border Gateway Protocol, peering and routing policies.
- **Single** [[docs/networks/VPC]] **target**.

#### Con
- Network latency.
- Variability.
- Depending on internet.
- Customer managed endpoints need to implement failover manually.
- Customer device needs single hop BGP.

### AWS Transit Gateway + VPN
- ***Over internet***
- **AWS** managed
- regional **router** distributes traffic to **different** [[docs/networks/VPC]]
- VPC need to be in the **same** region
- multiple customer gateways' for one AWS Transit Gateway

#### Pro
- Same as AWS Managed **VPN**.
- **Additional** high availability and scalability.
- **Up** to 5k attachments for the transit gateway.

#### Cons
- same as AWS Managed  **VPN**.

### AWS [[DirectConnect (DX)]]
- Dedicated network connection over private lines
- uses [[VirtualInterfaces]] in addition to customer gateway
- need multiple AWS direct connect connections to support multiple customer entry points, but only one virtual private gateway on AWS side
- higher bandwidth.
- Using private IP.
- 1 to 10 Gbps
- can use link aggregation group
- Use direct connect transit Gateway to connect to multiple regions or accounts or [[docs/networks/VPC]]

#### Pros
- More predictable Network performance
- Reduced bandwidth costs
- Support BGP peering and routing policies

#### Cons
- Requires additional telecom infrastructre

### AWS Transit Gateway + AWS [[DirectConnect (DX)]]
- dedicated private network connection to region router which distributes the traffic to multiple vpcs

#### Pros
- Same as AWS [[DirectConnect (DX)]]
- additional high availabilty and scalabity 
- up to 5k attachments for the transit gateway

#### Cons
- Same as AWS [[DirectConnect (DX)]]

### AWS [[DirectConnect (DX)]] + VPN
- Ipsec VPN connection over private Lines

#### Pros and Cons
- all Pros and cons of AWS Mangend VPN and AWS [[DirectConnect (DX)]]

### AWS [[DirectConnect (DX)]] + VPN + Transit Gatway
- Same as AWS [[DirectConnect (DX)]] + VPN but for up to 5k targets

### AWS VPN Cloud Hub
- Connect remote branch offices in a hub-and-spoke model for primary or backup connectivity
- connect remote to remote to remote to vpn

#### Pros
- Reusus exsiting internet connection and AWS VPN connections
- AWS managed and highly available
- Supports BGP for exchaning routes and routing policies

#### Cons 
- Network latency
- variablility and avialabilty are dependend on internet
- User managed branch office endpoints are responsible for failover implementation

### Software Site to Site VPN
- Software applicance-based VPN connection over the internet

#### Pros
- supports wider range of VPN vendors, products and protocols
- Fully customer manged solution

#### Cons
- customer is responsible for implementing high availabilty for all endpoints

## IPSec
- also known as Site to Site VPN
- connect to a vpc from on premise/remote

### Virtual Private Gateway
- also known as VPN Gateway
- entrypoint to AWS [[docs/networks/VPC]] side of your VPN Connection

### VPN Tunnel
- encryted link where data can pass from the customer network to, or from aws

### Customer Gatway
- An AWS Ressource that provides Information to AWS about your Customer Gateway device

### Customer Gateway Device
- Physical or Software
- On customer side (on premise/remote) to establish VPN connection


