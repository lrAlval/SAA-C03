

# VPC


### Site-to-Site VPN

#### Virtual Private Gateway VGW

#### Customer Gateway Device (on-premises)
- if customer gate is behind public ip , use public ip
- if is behind private IP, use the public IP of the NAT device that's enabled for traversal (NAT-T)
- enable **route propagation** for **VGW** in the route table that is associated with your **subnets**
- if you need to ping your EC2 instances from on-premises.
	- Enable ICMP protocol on the inbound of your [[SecurityGroup]]