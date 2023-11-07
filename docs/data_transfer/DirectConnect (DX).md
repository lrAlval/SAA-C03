![[Pasted image 20221031105646.png]]
# Direct Connect
- dedicated private connection from remote network to **VPC**
- Dedicated connection must be set between DC and AWS direct connect locations.
- Need Virtual Private Gateway on VPC.
## TLDR
Direct connect is a dedicated **connection** from on premise to AWS, which does not use the **internet**. It is expensive to set up and charged for GB out and in of AWS. It also takes at least a **month** to set up.
- Data in-transit not encrypted by default
	- AWS Direct Connect + VPN provides an IPsec-encrypted private connection
-  takes longer than a month to set up
- expensive
- charged per GB in and out of AWS.
- Dedicated connection from on premise to AWS.
## Use Cases.

- Increase bandwidth throughput 
	- working with large data sets
	- lower cost
- More consistent network experience
	- apps using real-time data feeds.
- Supports Hybrid Environments (on prem + cloud)

### Direct Connect Gateway
- useful to connect multiple VPCs from different regions.
![[Pasted image 20231018181104.png]]


## Resiliency

### High Resiliency for critical workloads
- two Direct Connections

![[Pasted image 20231018181832.png]]
### Maximum Resiliency for critical workloads
- two direct connect locations with two connections each.

![[Pasted image 20231018181838.png]]

## Connection Types
- both connection types take longer than 1 month to establish
### Dedicated Connections:
- 1 Gbps, 10 Gbps and 100 Gbps capacity
- physical ethernet port dedicated to a customer
- request made to AWS first, then completed by AWS Direct connect Partners

### Hosted Connections
- 50 Mbps, 500 Mbps to 10 Gbps
- Connection request are made via AWS Direct Connect Partners
- Capacity can be **added or removed on demand**.
- 1,2,5, 10 Gbps available at select AWS Direct Connect Partners.


## Fallback
In case Direct Connect fails, you can use the following as a fallback connection method:

![[Pasted image 20231018182118.png]]
## Direct Connection (Expensive)
- set up another Direct connection as a fallback, but it can be quite expensive
- one benefit is that it uses a dedicated private connection.

## Site-to-Site VPN
- connected through public internet using site to site vpn.
![[Pasted image 20231018182201.png]]