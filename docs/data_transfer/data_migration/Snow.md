![[Pasted image 20221031104435.png]]
# AWS Snow Family

## TLDR
The Snow **Familiy** is a collection of **hardware** which can be used to transfer large amounts of data into or out **aws**. Alternatively this hardware can also be used as data storage and computing power in locations where there is not internet (Edge).

## Solves
- Massive data migrations (10 Tb - 1 PB)

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
- big box to move tb or Petabytes of data in and out of **aws**
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
- Snowcone SSD - 14TB of SSD
- fits on top of a **drone**
- can transfer via network as well (collect offline transfer online)
- can be sent back to AWS offline or connect to internet and use [[DataSync]]

### Snowmobile
- **truck** to transfer data
-  Each **100PB** of data
- high security, temp controlled, GPS, 24/7 video surveillance
- use when transferring more than **10 PB**
![[Pasted image 20230530201554.png]]
## Edge Computing
- process on edge location
	- a truck on the road
	- a ship on the sea
	- a mining station underground
- no internet access
- preprocess

### Snowcone
-2 cpuss, 4gb on memory

### Snowball Edge
- runs [[EC2]] or [[Lambda]] functions

#### compute optimzed
- 52vCpus 208GiB Ram

#### storage optimized
- up to 40 vCpus, 80GiB of Ram

## Ops Hub
- GUI Software to connect to snow devices
- edge computing 
- store data for transfer