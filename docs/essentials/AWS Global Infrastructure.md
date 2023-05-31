## Regions

- A region is a geographical area.
- Each region consists of 3 or more availability zones.
- Each Amazon Region is designed to be completely isolated from the other Amazon Regions.
- Each AWS Region has multiple Availability Zones and data centers.
- You can replicate data within a region and between regions using private or public Internet connections.
- You retain complete control and ownership over the region in which your data is physically located, making it easy to meet regional compliance and data residency requirements.
- Note that there is a charge for data transfer between regions.
- When you launch an EC2 instance, you must select an AMI that’s in the same region. If the AMI is in another region, you can copy the AMI to the region you’re using.


## Availability Zones

- Availability Zones are physically separate and isolated from each other.
- AZ's span one or more data centers and have direct, low-latency, high throughput, and **redundant** network connections between each other.
- Each AZ is **designed** as an **independent failure zone.**
- When you launch an instance, you can select an Availability Zone or let AWS choose one for you.
- If you distribute your EC2 instances across multiple Availability Zones and one instance fails, you can design your application so that an instance in another Availability Zone can handle requests.
- You can also use Elastic IP **addresses** to mask the failure of an instance in one Availability Zone by rapidly **remapping** the address to an instance in another Availability Zone.
- To ensure that resources are distributed across the Availability Zones for a region, AWS independently map Availability Zones to names for each AWS account.
	- For example, the Availability Zone **_us-east-1a_** for your AWS account might not be the same location as us-east-1a for another AWS account.

- To coordinate Availability Zones across accounts, you must use the **_AZ ID_**, which is a **unique** identifier for an Availability Zone.
- AZs use **discrete** **UPS** and **onsite backup** generation facilities and are fed via different grids from independent facilities.
- AZs are all redundantly connected to multiple tier-1 transit providers.
- The following graphic shows three AWS Regions each of which has three Availability Zones:
![[Pasted image 20230530165502.png]]

## Local Zones

- AWS Local Zones: Place compute, storage, database, and select AWS services closer to end-users.
- Highly Demanding Applications: Run applications with single-digit millisecond latencies using AWS Local Zones.
- Extension of AWS Region: Each Local Zone location is an extension of an AWS Region.
- Latency Sensitive Applications: Run latency-sensitive applications in Local Zones.
- Supported AWS Services: 
	- Amazon Elastic Compute Cloud (EC2), 
	- Amazon Virtual Private Cloud (VPC), 
	- Amazon Elastic Block Store (EBS), 
	- Amazon File Storage, and 
	- Amazon Elastic Load Balancing are supported in Local Zones.
- Geographic Proximity: Local Zones allow running applications in geographic proximity to end-users.
- High-Bandwidth Connection: AWS Local Zones provide a high-bandwidth connection between local workloads and the AWS Region.
- Seamless Connectivity: Connect to the full range of in-region services seamlessly.

## AWS Wavelength

- AWS Wavelength enables developers to build applications that deliver single-digit millisecond latencies to mobile devices and end-users.

- AWS developers can deploy their applications to Wavelength Zones, AWS infrastructure deployments that embed AWS compute and storage services within the telecommunications providers’ datacenters at the edge of the 5G networks, and seamlessly access the breadth of AWS services in the region.

- AWS Wavelength brings AWS services to the edge of the 5G network, minimizing the latency to connect to an application from a mobile device.

## AWS Outposts

- AWS Outposts bring native AWS services, infrastructure, and operating models to virtually any data center, co-location space, or on-premises facility.

- You can use the same AWS APIs, tools, and infrastructure across on-premises and the AWS cloud to deliver a truly consistent hybrid experience.

- AWS Outposts is designed for connected environments and can be used to support workloads that need to remain on-premises due to low latency or local data processing needs.

## Edge Locations and Regional Edge Caches

- Edge locations are Content Delivery Network (CDN) endpoints for CloudFront.
- There are many more edge locations than regions.
- Currently, there are over 216 edge locations.
- Regional Edge Caches sit between your CloudFront Origin servers and the Edge Locations.
- A Regional Edge Cache has a larger cache-width than each of the individual Edge Locations.

![[Pasted image 20230530165609.png]]