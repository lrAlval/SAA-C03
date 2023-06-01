![[Pasted image 20221031104435.png]]
# AWS Snow Family

![[Pasted image 20230531191203.png]]

## TLDR
The Snow **Familiy** is a collection of **hardware** which can be used to transfer large amounts of data into or out **aws**. Alternatively this hardware can also be used as data storage and computing power in locations where there is not internet (Edge).

## Solves
- Massive data migrations (10 Tb - 1 PB)

## Caveats
- Snowball cannot import to Glacier directly
- Must import to [[S3]] first, then move to Glacier with a lifecycle policy.

## Use cases
- data migration
	- **Snowcone**
	- Snowball  Edge
	- Snow mobile
- Edge computing
	- Snowcone
	- Snowball Edge

## Data migration
- Used when network lines are not fast enough (**TBS** and **PBS**)
- recommended if data migration takes more than one week

### Step by Step
- Request a **device** from AWS
- Install ops software on your servers
- Use the **client** and **hardware**
- Ship back
- Snow device is **wiped**

## Devices

### Snowball Edge
- big box to move tb or Petabytes of data in and out of **AWS**
- large data cloud migrations, decommission a data center, disaster recovery
- pay per job
- provide block or [[S3]] compatible storage
- cluster up to 15 devices (like 1 PB)

#### Storage optimized
- 80 TB of HDD

#### Compute optimized
- 42 TB  of HDD or 28Tb **NVMe** 

### Snowcone
- Smaller Snowball
- Snowcone 8TBs of storage
- Snowcone SSD - 14 TB of SSD
- fits on top of a **drone**
- can transfer via network as well (collect offline transfer online)
- can be sent back to AWS offline or connect to internet and use [[DataSync]]

### Snowmobile
- **truck** to transfer data
-  Each **100 PB** of data
- high security, temp controlled, GPS, 24/7 video surveillance
- use when transferring more than **10 PB**
![[Pasted image 20230530201554.png]]
## Edge Computing
- process on edge location
	- a **truck**  on the road
	- a ship on the sea
	- a mining station underground
- No internet access
- preprocess
- All snow family can run ec2 instances & AWS lambda functions 
	- using **AWS IoT Green grass**.
- 1 – 3 years discounted pricing.

#### Use case
- Preprocess data
- Machine learning at the edge
- Transcoding **media** **streams**.
- Eventually, if needed, we can ship back the device to **AWS** (for transferring data e.g.,) 

### Snowcone & Snowcone SSD
- 2 CPUs, 4gb of memory, wired or wireless access

### Snowball Edge – Compute Optimized
- runs [[EC2]] or [[Lambda]] functions
- 104 vCPUs, 416 GiB of RAM
- Optional **GPU** (useful for video processing or machine learning)
- 28 Tb NVMe or 42 TB **HDD** usable storage
- allow pre-processing of data.

#### Storage optimized
- up to 40 vCPUs, 80 GiB of Ram
- Object storage clustering available.

## Ops Hub
- GUI Software to connect to **snow devices**
	- unlocking and configuring single or clustered devices
	- Launch compatible AWS services on your devices
		- [[EC2]]
		- [[DataSync]]
		- Network file system (NFS)
	- transferring files
	- launching and managing instances running on snow family devices
	- monitor devices metrics 
		- storage capacity
		- active instances on your device
- edge computing 
- store data for transfer