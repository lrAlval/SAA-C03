![[Pasted image 20221101124548.png]]
# RDS

## TLDR
Various  relational databases, managed by AWS.
Supported DBs:
- Postgres
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- Aurora (AWS proprietary database)

## Features
- **Scaling capacity** auto enables when: 
	- needs a predefined maximum **storage threshold**. (22Gbs - 6144Gbs)
	- Useful for apps with **unpredictable workloads**
	- auto enables when: 
		- Free storage is less than 10% allocated storage
		- low-storage last at least 5 mins.
		- 6 hours have passed since **last modification.**
- OS patching
- OS & database managed by AWS
- no ssh
- monitoring dashboards
- **multi AZ**
- **scaling capability.**
- Storage backed by [[EBS]] (GP2,io1)

## Read replicas
- up to **15** read replicas
- Within **AZ**, Cross **AZ** or cross **Region**
- replication is **Async** so reads are **eventually** **consistent**.
- Can be promoted to their **own database**
- Apps must update connection string to leverage **read replicas**.
- No network cost for **cross AZ** in the same **region**.
- **Cross region** **cost per** network traffic.
- Can be **multi AZ** (helpful for **[[docs/essentials/Resilience concepts#Disaster Recovery (DR) ☠️|DR]]**)
![[Pasted image 20230523161209.png]]

## RDS Multi AZ (failover) (Disaster Recovery at az)[[docs/essentials/Resilience concepts#Disaster Recovery (DR) ☠️|DR]] 
- **__SYNC replication__**
- can be upgraded **without** **downtime** (from Single **AZ** to **Multi-AZ**)
- the read replicas can also be setup as **multi AZ** for DR
- **one** **DNS** name
- **automatic** **failover** to **standby** database by switching target IP of DNS name
- one Db. will be standby
- deactivate automation mode and take snapshot before modify
- **automated** **backups** will be multi region

![[Pasted image 20230523161750.png]]

## RDS Custom
- only for **oracle** and **MySQL**
- full admin access to the underlying OS and database
- access to underlying database and OS
	- install patches
	- enable native features
	- configure settings
	- access underlying ec2 instance using **ssh** or **ssh session manager**
- ssh possible

## Security
- if you need to **encrypt** in transit use SSL/TLS by launching the client with the --SSL_ca flag
- can use [[KMS]] to encrypt data at rest

### Option

#### RDS Custom for Oracle
- allows customization to host and OS

## Maintenance 
- causes **downtime** even if the db is multi AZ

## Backups
- daily full backup during **maintenance** window
- transactions logs are backed up by **RDS** every **5 mins**
- restore any point in time (from the oldest backup to 5 mins ago)
- 1 to 35 days of retention
- back-ups **can be disabled**.
- If **multi AZ** backups span **multi region.**

### Manual Snapshot
- manually **trigger**
- retention as log as you want.

### Savings
- in a stopped RDS database, AWS still **charges** for **storage**.
- Take **snapshot** and **delete** **database**
	- if you want **RDS** back, just restore with **snapshot**.

### Restore 
- MySQL RDS database from [[S3]]
- Restore backup file onto new RDS instance running MySQL

## Security
- encrypt **at rest** with [[KMS]], must be defined at launch time
- if **master is not encrypted**, **read** **replicas** can not be encrypted
- to change from and to encrypt **restore a snapshot as encrypted**
- encrypt **in flight** with TLS root **certificates**' client side
- can use [[IAM]] **roles** to connect to database instead of **username** and PW
- can use [[SecurityGroup]]
- audit logs can be enabled and be sent to [[CloudWatch]]


## RDS Proxy
- fully **managed** **database** **proxy** 
- allows apps to **pool** and **share connection** established with the database, which allows **less connections** to database.
- Improves database performance
- **serverless**, autos calling, **high available** (multi AZ)
- reduces **RDS** and aurora **failover** time by **66%**
- enforces IAM auth for db and store creeds in AWS secrets manager
- RDS Proxy is never public and can only be used from **within** the [[VPC]]

## Enhanced Monitoring
[[CloudWatch]] feature for RDS

- RDS child processes
- RDS processes
- OS Processes
