
- Enables creation of a private connection between VPC to supported AWS services and VPC endpoint services powered by ***PrivateLink*** using its private IP address. 
- **Traffic** between VPC and AWS service does not leave the Amazon network.

## Key points

- VPC endpoint enables users to privately connect their VPC to supported AWS services.
- VPC Endpoint does not require a public IP address, access over the Internet, NAT device, a VPN connection or AWS Direct Connect to communicate with resources in the service.
- Endpoints are virtual devices, that are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in the VPC.
- Access to the resources in other services can be controlled by endpoint policies.
- By default, Endpoint policy, allows full access to the service. Endpoint policies must be written in JSON format.
- Endpoint policy does not override or replace IAM user policies or service-specific policies (such as S3 bucket policies).