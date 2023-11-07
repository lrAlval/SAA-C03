 ![[AWS-Networking-Content-Delivery-Services.png]]
- **CIDR**: IP Range
- **IPsec**: **protocol** suite for securing **IP** communications by authenticating and encrypting **each IP packet** of a data **stream**.
- **VPC**: Virtual Private Cloud
	- define a list of IPv4 & IPv6 **CIDR**
	- **logically isolated portion of AWS cloud** within a **region**.
	- Resiliency => **Region**.
	
- **Subnets**: 
	- tied to a **single AZ**, we define a **CIDR**.
	
- ***Internet Gateway***: 
	- at the **VPC** level, provide IPv4 & IPv6 Internet Access.
	
- **Route Tables**
	- map **interconnections** between **subnets** and map direct **traffic** between **gateways** (IGW, VPC Peering Connections, VPC Endpoints) and **subnets**.

- **Bastion Host**: server whose purpose is to **provide** **access** to a private network from an external network.
	- **Public** **EC2** instance to **SSH** into, that has an **SSH** connectivity to EC2 instances in private **subnets**.
	
- **NAT Instances.** (Deprecated but still in exam): 
	- Gives **internet access** to instances in **private subnets**. 
	- ***Old***, must be set up in a ***public subnet***, disable `Source / Destination check` flag
	
- **NAT Gateway**.
	- Managed Network Address **Translation** to resources in **private subnets** that need access to **internet**.
	- ***Resiliency →*** specific to **AZ**, using **Elastic IP**.
		- To have **high availability**, we should create a **NAT** **gateway** in **each** **AZ**.
	- No need to disable **source/destination** check.
	- **IPv4 only**.
- **Network access control lists - NACL**
	- **Stateless**.
	- Subnet rules for both **inbound** and **outbound**.
	- NACLs **deny** all inbound **and** **outbound** traffic by **default**, but support both **allow** and **deny** rules.
	- Pay attention to the **Rules** Order, Rules are **evaluated** from **top** to **bottom**, first match wins, on match fail goes to the **next**.
- **Security Groups**
	- Stateful **firewall**
	- only **Allows** rules.
	- Evaluated as a **whole**.
	- Operate at the EC2 instance level.
		-  one SG can be applied to instances in **diff** **subnets**.

## VPC Connectivity

- **VPC Peering**
	- connect **two** **VPCs** with non overlapping **CIDR**
	- non-transitive (1-1 **connection only**).
	- Traffic **always** stays on the global **AWS** **backbone**, and **never** traverses the public internet.
- **AWS Classic Link**
	- Allows you to link an **EC2-Classic** instance to a **VPC** in your account, within the same **region**. 
	- This allows you to associate the **VPC** security groups with the EC2-Classic instance, enabling communication between your EC2-Classic instance and instances in your VPC using private IPv4 addresses.
- **VPC Endpoints**
	- enable private connectivity to **services** hosted in AWS from the VPC (without using Internet Gateway, VPN, NAT, etc)
	- (Interface and Gateway) allow you to **privately** access AWS services using AWS internal network (backbone) **instead** of traversing the ***public internet***.
	- **Gateway endpoints**:
		- **Free Service.**
		- **Targets** in a **Route table** that redirect **traffic** to specific AWS services ( currently just **S3** and **DynamoDB**)
	- **Interface endpoints**:
		- essentially ENIs (Elastic Network Interfaces) (Virtual Network Cards) with a private **IP**.
		- Rely on **AWS PrivateLink** to allow private and secure connection between VPCS, on-premise and AWS services.
- **AWS Client VPN**
	- allows you to access your AWS resources inside a VPC
- **Hardware VPN Connection**: 
	- Hardware-based VPN connection between your datacenter / location and the VPC.
- **AWS Site to Site VPN**
	- By default, instances inside a VPC can't communicate with your own **remote** **network**.
	- Setup can be a 
		- Customer Gateway on a Direct Connection.
		- Virtual Private Gateway on a **VPC**.
		- Site-to-site over public internet.
	- You can enable access **to** your remote network from your VPC by creating an AWS Site-to-Site VPN (Site-to-Site VPN) connection
	- **Site-To-Site VPN** requires a **Customer Gateway Device** (physical or software) on the Client Side of the VPN (your network / office / data-center ) plus a **Customer Gateway** on AWS to provide AWS with the info about your device) and a **Virtual Gateway** on the Amazon side of the VPN.
	- The VGW (Virtual Private Gateway) is attached to the VPC and then it can communicate with the Customer Gateway via VPN Tunnel.
		- ***Virtual Private gateway***: Amazon side of a VPN connection, 
		- ***Customer Gateway***:  the customer side of it.
- AWS VPN **Cloud** **Hub**:
	- when you want multiple remote offices to connect to a vpc or aws resources in a **hub-and-spoke** model
	![[Pasted image 20231020162535.png]]
- **AWS Direct Connect** (DX):
	- **Build Hybrid Networks**
	- uses private **network** connections (AWS Backbone) in to the AWS Cloud and is **high-bandwidth** and **low-latency**.
	- private connectivity between **AWS** and your data-center/office (it uses AWS **backbone**)
	- increased speed/latency and **bandwidth**/throughput.
	- cost effective if transferring large **volumes** of data from your data center to AWS.
	- **Cons**: are that it is **costly** and requires **additional** telecom and hosting provider relationships
	- **Cons**: [traffic (in transit) NOT ***encrypted*** by ***default***](https://docs.aws.amazon.com/directconnect/latest/UserGuide/encryption-in-transit.html).  if you need encryption you will need an **IPSec** **Site-to-Site** **VPN** **connection** over a **VIF** (Virtual Interface).
- **VPC Flow Logs**:
	- helps to identify attacks, **analyze** using [[Amazon Athena]] or [[CloudWatch]].
	- can be setup at the 
		- **VPC**  
		- Subnet 
		- ENI Level for **ACCEPT** and **REJECT** traffic, 
		-






## FAQs
https://aws.amazon.com/vpn/faqs/


https://dev.to/aws-builders/aws-virtual-private-cloud-vpc-cheat-sheetwrite-up-1i8b
## CIDR guidelines/considerations

- Block **size** must be between /16 and /28
- CIDR block must not overlap any existing blocks associated with the VPC
- CIDR block size can't be increased or decreased
- AWS recommends using **CIDR** blocks from **RFC 1918** ranges for private **networks**:
	- 192.168.0.0 – 192.168.255.255 (192.168/16 prefix)
		- 256 contiguous class **C**.
	- 172.16. 0.0 – 172.31. 255.255 (172.16/20 prefix) 
		 - 16 contiguous class **B**.
	- 10.0.0.0 – 10.255.255.255 (10.0/24 prefix) 
		 - single network class **A**.
- when setting the size of the subnets keep in mind that **first four and last IP addresses are not available** for use
- **bigger** CIDR blocks give more flexibility but smaller subnets are ok for most use cases
