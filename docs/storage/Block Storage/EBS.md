![[Pasted image 20221101204757.png]]
# Elastic Block Store

## TLDR
- This is network storage attached to an [[EC2]] instance.

## Features
- EBS (Elastic block store) **Volume** is a **network** drive you can attach to your instances while they run.
- **Network Drive**
- can only be mounted to one instance at once 
	- (Except io1 & io2 which can use [[EBS#EBS Multi attach|multi-attach]] feature)
- limited to **AZ** which it was **created**
- can be **attached** and **detached** quickly
- need **snapshot** to **move AZ**
- Uses **provisioned** **capacity** (Size and IOPS)
- you get **billed** even if drive is not full
- **persist Data** after Termination
- **delete on termination** is an option
- can be **modified** while in use (**IOPS** and **capacity**)

## EBS Volume
 - **Network Drives** with good but “**limited**” performance
 - **locked** to an **AZ**, (Except if using a **snapshot**)
 - can be **attached** and **detached** quickly
 - have provisioned **capacity** (size in **GBS** & **IOPS**)
	 - **billed** for all **provisioned** **capacity**
	 - can increase the **capacity** of the drive over time
 - **delete EBS volume on termination** is an option.

## Snapshot
- is a Backup, can be done during **attachment**
- **Backups** can be **restored** to other **regions** or **AZ**
- **snapshot** can be done while the **volume is being used**

### EBS Snapshot Archive
- cheaper **Snapshot** **storage** but longer restore time
- takes within **24** to **72** **hours** for **restoring** archive

### EBS Recycle Bin
- can enable recycle for recovery (retention 1day - 1 year)
- allow to setup rules to retain deleted snapshots for accidental deletion.

### Fast Snapshot Restore (FSR)
- force full initialization of snapshot to have no **latency on restore**
- useful when your snapshot is massive and need to initialize an EBS volume with **no latency**
- **cost** a lot
- no **latency** with restore

## Volume types
- only **SSD** volumes can be used as boot volumes
- Only GP2/GP3 and io1/io2 can be used as **boot volumes**.
- Each type varies in:
	- Size
	- Throughput
	- IOps (I/O Ops per sec)
- can come in 6 types
- gp2/gp3 (SSD): **General** purpose **SSD** 
	- balances price & performance.
	- **Wide** variety of **workloads.**
- io1/io2 (**SSD**): **Highest-performance SSD** 
	- mission-critical low latency 
	- high-throughput workloads
- st1(HDD): **Lowest cost** HDD designed 
	- less frequently accessed workloads.
- sc1(HDD) **Lowest** cost HDD 
	- designed for less frequently **accessed** workloads

### General Purpose GP2/GP3 (SDD)
- general purpose SSD
- cost effective Storage, l**ow latency**
- System **boot** **volumes**, virtual desktops, development and test environments.
- 1 GiB - 16 TiB

#### gp3
- baseline of **3k** iops and 125 mibs
- can be increased to 16k iops and 1k mibs

#### gp2
- small 
- burst up to 3k iops
- size of volume and iops are linked up to 16k iops max
- 3 iops per gb

### Provisioned IOPS (PIOPS) IO1/IO2
- high performance SSD
- supports EBS [[EBS#EBS Multi attach|multi-attach]]
- mission critical, low latency
- Great for **databases workloads** (**sensible to sorage perf and consistency**)
- 4Gib - 16TiB
- max piops 64k for nitro ec2 
- max piops 32k for non nitro
- io2 is just better
- iops gb ratio 50:1 (10GB max 500 iops)

#### io2 block express
- sub milisecond latency
- max piops 256k 
- iops gb ratio of 1000:1

### Hard Disk Drives (HDD)
- cannot be a **boot volume**

#### **Throughput optimized hdd** (st1)  
- low cost hdd volume
- 125mb - 16 tb
- designed for frequently access and throughput intensive
- low cost
- bit data workloads , data warehouses, log processing
- max 500mbs and 500 iops

#### Cold HDD sc1
- hdd less frequently accessed workloads (lowest cost)
- cold ssd
- 250mbs and 250 iops


### Instance Store
- highest performance but ephemeral
- is lost even on hibernation
- cannot be **detached** and **attached** to other [[EC2]]

## EBS Multi attach
- Same **AZ** can **attach** same volume to multiple **instances**
- application must manage **concurrency**
-  Achieve [[docs/essentials/Resilience concepts#High Availability (HA) **🏷️**|High Availabilty]]
- only available for **io2** and **io1**
- each instance has full permissions
- **cluster** Linux applications
- max of **16** [[EC2]] instances
- file system must be cluster aware

![[Pasted image 20230521221627.png]]

## EBS Encryption
- Data **at rest** is **encrypted**
- Data is encrypted **in flight** between [[EC2]] and [[EBS]]
- **Snapshot** is encrypted
- Volumes created from encrypted snapshot are encrypted aswell
- handles by aws behind the scenes
- minimal impact of latency
- uses keys from [[KMS]] (AES-256)
- copying and **unencrypted** snapshot **enables** **encryption**

### Encrypt currently not encrypted
- created snaphsot
- encrypt snapshot
- create volume from snapshot
- attach new volume

## Raid

### Raid 0
- when  **IO** is more important than [[docs/essentials/Resilience concepts#Fault-Tolerance (FT) 💰|Fault Tolerance]].
### Raid 1
- when  [[docs/essentials/Resilience concepts#Fault-Tolerance (FT) 💰|Fault Tolerance]] is more important than IO
