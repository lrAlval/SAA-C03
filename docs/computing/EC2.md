![[Pasted image 20221030223457.png]]
# Elastic Compute Cloud

## TLDR
EC2 is a the combination of a virtual mashine and hardware capacity attached to that vm in AWS. It is one of the oldest services and well integrated into most other services.

## Virtual Machines (EC2)

### Configuration Options
- OS (Win, Linux, MacOs)
- CPU
- RAM
- Network attached storage ([[EBS]] & [[EFS]])
- can have multiple [[EBS]] attached storage
- Hardware attached ([[InstanceStore]])
- Network Card (Speed, Ip)
- Firewall ([[SecurityGroup]])
- Bootstrap script (User Data)

### User Data
- Is a script is run once on the first start of the instance
- Script is run using root privileges

### Use Cases
- Installing updates
- Installing software
- Download files from the internet

### Instantiating EC2 Instances quickly
- Use Golden AMI(pre-configured AMI with all dependencies installed)
- Boostraping using User data : For dynamic config, user data scripts
- Hybrid: mix Golden AMI and User Data [[ElasticBeanstalk]]

### Instance Types
- https://instances.vantage.sh/

#### Type Definition
- Split by family
- In family types are defined by Class.Generation.Size 

## Families

#### General Purpose
- Balance between, computing, memory and network speed

#### Compute Optimized
- e.g instance name c6g => (where c stands for cpu)

##### Use cases
- High cpu power
- batch processing workloads
- media transcoding
- high performance web servers
- high perfomance computin (HPC)
- Scientific modeling & machine learning
- dedicated gaming servers

#### Memory Optimized 
- e.g instance name r6g => (where R stands for Ram)
- High amount of RAM/Memory

##### Use cases
- high performance relational / non relational databases
- distributed web scale cache stores
- In-memory databases optimized for BI
- Applications performing real-time processing of big unstructured data
- Process large data sets in memory
- Cache stores

#### Storage Optimzied
- High amount of Disk IOPs
- Great for storage-intensive tasks that require high, sequential read and write acccess to large datasets on local storage.

##### Use cases
- High frequency online transaction processing systems (OLTP)
- Relational & NoSQL databases
- Cache for in-memory databases (e.g redis)
- Data warehousing apps
- Distributed file systems.
- Alot of Datasets in local storage


## Purcharsing Options
- On-Demand Instances - short workload, predictable pricing , pay by second.
- **Reserverd** ( 1 & 3 years)
	- **Reserved Instances** - long workloads
	- **Convertible Reserved Instances** - long workloads with flexible instances
- **Saving Plans** (1 & 3 years)
- **Spot Instances** - short workloads, cheap, can lose instances (less reliable)
- **Dedicated hosts** - book an entire physical server, control instance placement
- **Dedicated Instances** - no other customer will share your hardware.
- **Capacity Reservations** - reserve capacity in a **specific AZ** for any duration.

![[Pasted image 20230521134644.png]]

### On Demand \$\$\$\$

 best for **shor-term** and **un-interrupted** workloads, where you can't predict how the app will behave.

- Pay for what you use:
	- Linux or windows - billing per second, after the first minute.
	- all other OS - billing per hour.
- has the **highest cost** but **no upfront payment**
- **no long-term** commitment
- Use for **short** **workload**

### Reserved

#### Default
Recommended for steady-stage usage aps e.g database

- Up to **72%** discount compared to **on-demand**.
- **Cheaper** if payed upfront & Cheaper than on demand.
- Need to specify type os, region, tenacy
- **Reservation Period** - 1 year (+ discount) or 3 years (+++)
- **Payment Options** - No Upfront (+), Partial Upfront (++), All Upfront (+++)
- **Reserved Instance Scope** - **Regional** or **Zonal** (reserve in zone and AZ)
- You can buy or sell in the **Reserved Instance**  marketplace.


#### Convertiable
- Up to **66%** discount
- More **expensive** than default
- Can change instance **type**, os, **region**, **tenacy**

### [[SavingsPlans]]
- 1 Year OR 3 Years
- Get a discount based on **long-term** usage (up to 72% - samge as RIs)
- **_Commit_** to a certian type of **usage** ($10/hour for 1 or 3 years)
- **_usage beyond_** commit is **billed** on **demand price \$\$\$\$**
- Locked to instance family and region
- Commit to an amount of usage (cpu, mem, disk)
- Flexible (can change)
	- Instance Size (m5.xlarge, m5.2xlarge)
	- OS (Linux, windows)
	- Tenancy (Host, dedicated, default)

### Spot Instances
Useful for workloads that [[docs/essentials/Resilience concepts#Fault-Tolerance (FT) 💰|Fault Tolerant]]
- discount of up to **90%** vs on-demand.
- **Cheapest of all types**
- Instances **_can be lose_** at any point in time.
- MOST **cost-efficient** instances in AWS.
- Define **max price** you are willing to pay:
	- if you are overbid your instance is gone.
- at any time Can lose instance

#### Use Cases
- Short workloads
- batch jobs
- Suited for **resiliant** jobs
- Image processing 
- Data analysis 
- Distributed workloads (these are resiliant by definition)
- workloads with a flexible start and end time.
- **not suitable** for critical jobs or databases.


### Dedicated Hosts
- Rent an entire physical server, control placement of that server
- allows address **compliance requirements** and use your existing server software licenses (per-socket , per-core, per VM software licenses)
- useful for software that have complicated licensing model (**BYOL**- bring your own license)
- can use on demand or reserved.
- most expensive 
- can convert to dedicated instance

#### Use Cases
- Complicance
- Server bound software licences

### Dedicated Instances
- No other customer will share the hardware used by you
- Hardeware may be shared within **same** account
- No **control** over **instance** **placement** (can move hardware after Stop /start)
- can convert to **dedicated** **host**

### Capacity Reservations
- Reserve a capacity in a AZ for duration (on demand instance)
- No time commitment
- No billig discount
- Combine with Saving plan and Reserved Instances for same AZ to save money
- **Charged**  at **on-demand rate** whether you run instances or not.

  #### Use Cases
- short term **uninterrupted** workload in a specific az

## Spot Instance
- Request for an instance and the instance running itself is diffrent 
- spot request can either be one time or persistent
	- persistent request will continue supply of instances until a vlid time and desired number of instances are fullfilled.
- define **max spot price** and get instance while **current spot price** < max
	- hourly spot price varies based on offer and capacity
	- if current spot price > max_defined_price - you can either **stop** or **terminate** your instance with a **2 minutes** **grace** period.
- If you terminate your instance but not the **request** the instance will be **relaunched**
- can only cancel a spot request , if the request is either in open , active or disabled.
- If you cancel your request your instance **will** **still** be **running**
![[Pasted image 20221101164159.png]]
### Spot Blocks (Deprecated)
- Duration window of your Spot instance 
- **1 to 6 hours**
- designed to not be **interrupted**
- still not garanteed 

### Fleet
- define launch pools : instance type , OS , AZ.
- Define a budget and target capacity
- multiple launch pools
- Spot fleet stops launching instances when reaching capacity or max costs.
- allows us to auto request spost instances with the lowest price.

#### Strategies
- **Lowest price**, launch from lowest price pool
- **Diversified**, launch from all pools (resiliance)
- **Capacity optimized**, launch from pool with strongest capacity settings
- **price capacity optimized (recommended)** pools with highest capacity available, then select the pool with the lowest price(best choice for most workloads).

## Elastic Ip
- public static ip
- A static ip which can be attached to Elastic Network Interfaces and other services
- Used to mask a fail by keeping ip but changing machine
- Up to **5 per account**
- Can request more than 5 from aws

## Placement Groups
Placement strategy for a group ec2 instances

### Spread
- **Multi** **AZ** 
- **Diffrent** **hardware**
- Limited to **7** **instances** per **AZ**  **per placement group**
- Use for **critical** apps and [[docs/essentials/Resilience concepts#High Availability (HA) **🏷️**|High Availability]]

#### use case
- app that needs to maximize [[docs/essentials/Resilience concepts#High Availability (HA) **🏷️**|High Availability]]
- critical apps where each instance must be isolated from failure from each other.

![[Pasted image 20230521205236.png]]

### Cluster 
- all instaces are on the **Same** rack on same **AZ**.
- high-performance **networking**
- **Rack** **fail** -> **all EC2s fail**
- Fast **internal** connection from ec2 to ec2 
- Used for **low** **latency** and big data jobs with deadline
- Great network (10 Gbps **bandwith** between instances)

#### use case
- big data job that needs to complete fast
- app that needs **extremely** **latency** and high **network** **throughput**

![[Pasted image 20230521201634.png]]

### Partition
- **Multi** **AZ**.
- **Multi rack** but **same rack** **per partition**
- spread instances across many **partitions** within an **AZ**
	- each partition uses a different set of **racks**.
- scale to 100 EC2 instances per group (Hadoop, Cassandra , Kafka).
- failure is isolated at **partition level**.

#### Use Case
-  big data application which are partition aware (HDFS,HBase, Cassandra, Kafka)
![[Pasted image 20230521205633.png]]

## ENI Elastic Network Interfaces
- **Virtual Network Card**
- Can be used not only for ec2
- Eth0 = **primary ENI**
	- **Primary private IPv4**, one or more secondary **IPv4**
	- one elastic IPv4 per private IPv4
	- one public ipv4
	- one or more security groups
	- a mac **address**
- you can create ENI indepently and attach them on the fly (move them) on EC2 instances for **failover**.
- Can add multiple for **multiple private ips**
- Can attach **elastic ip**
- Can attach **mac** address
- Can **attach** and **detach** from **instance**
- **Bound by AZ**
![[Pasted image 20230521211256.png]]

### EFA Elastic Fabric Adapter
- use to accelerate high performance computing by providing os bypacc hardware interface
- cannot be used for windows 

### ENA Elastic Network Adapter
- use for high performance networking capabilitiies
- slower than efa

## EC2 Hibernate
- **Standby** for EC2, ram is **saved**
- **Faster** **startup**
- **Root** [[EBS]] must be encrypted
- Used for **breaks** in very **long running tasks** or if an **instances** takes very **long to startup**
- Can last **no longer than 60 days**
- Must be enabled before launch

## EC2 Instance Recover
- Creates a new EC2 instance which is identical to the previous ec2
- recovers private and public ip, metadat, elastic ip, instandce id
- data in memory is lost

## Limits
- by default your account has a maximum limit for **ec2** instances based on the **total vcpu used**, you can submit a request to increase that limit