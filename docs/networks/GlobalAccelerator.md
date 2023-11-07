
# AWS Global Accelerator

![[Pasted image 20221101170746.png]]
## TLDR
**UDP** compatible global endpoint to speed up network **traffic** to your [[docs/networks/VPC]] by using edge locations and **AWS** private network.

## Use case
- reduce network-hops for **worldwide users**.
- improve global network performance by offering entry point on to the global AWS transit network as close to customers as possible using Any cast IP addresses.

## Features
- **Global service**
- network layer service
- Intelligent **routing** to the lowest latency and fast regional **failover**.
- Internal **AWS network**
- No Issue with client cache (because the IP **doesn't** change)
- Distribute traffic to optimal endpoints over AWS Network
- two static **anycast** IP addresses as fixed entry points
- the **anycast** **IP** send traffic directly to edge locations
	- the edge locations send traffic to your application.
- Can use **weights** to distribute portion of traffic
- good fit for **non-HTTP** use cases.

![[Pasted image 20230530170706.png]]

## Targets
- [[ELB]], [[docs/scalabily/ELB#Application Load Balancer (ALB)|ALB]], [[docs/scalabily/ELB#Network Load Balancer (NLB)|NLB]]
	- public or private
- **Elastic IP**
- [[EC2]]

## Health Checks
- failover less than 1 min **unhealthy**
- good disaster recovery

## Security
- only 2 external IPs need to be white-listed
- **DDoS** protection thanks to [[AWSShield]]


