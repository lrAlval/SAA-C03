- RD BMS (SQL/ OLTP)
	- RDS, Aurora – great for **joins**
- NoSQL databases
	- DynamoDB (JSON)
	- ElasticCache (Key/value pairs)
	- Neptune (graphs)
	- DocumentDB (for MongoDB)
	- Key spaces (for Apache Cassandra)
- Object Store:
	- S3 – for big objects / blob storage
	- Glacier (for back-ups / archives)
- Data Warehouse SQL analytics / BI
	- Redshift (OLAP)
	- Athena
	- EMR
- Search
	- OpenSearch(JSON) – free text, unstructured searches
- Graphs:
	- Amazon Neptune – displays relationships between data.
- Ledger:
	- Amazon Quantum Ledger Database
- Time series:
	- Amazon Time stream

## Some criteria to focus
- read-heavy, write-heavy or balanced workload ?
- Throughput needs?
	- Will it change ?, does it need to scale or fluctuate during the day ?
- How much data to store and for how long ? 
	- Will it grow ?
	- Average object size ?
	- How are they accessed ?
- Data durability ?
	- Source of truth for the data ?
- Latency requirements ?
	- Concurrent users?
- Data Model ?
	- How will you query the data ?
		- Joins ?
		- Structured ?
		- Semi-structured?
	- Strong schema ?
	- More flexibility ?
- Reporting ?
- Search?
- RDBMS / NoSQL ?
- License costs ?
	- Switch to cloud native DB such as Aurora ?


## RDS
- Managed PostgreSQL
	- MySQL
	- Oracle
	- SQL server
	- MariaDB
	- Custom
- **Provisioned** RDS Instance Size and EBS Volume Type & Size
- Auto-scaling capability for **Storage**.
- Support for Read-Replicas and 
	- stand by **Multi-AZ** just for **failover** useful for Disaster recovery scenarios. 
- Security through IAM, Security Groups, **KMS**, SSL in transit.
- Automated back up with point in time restore feature (up to **35 days**)
- Manual DB Snapshot for longer-term recovery
- Managed and scheduled maintenance (with **downtime**)
- Support for **IAM Authentication**, integration with **Secrets Manager.**
- RDS custom for access to and customize the underlying instance 
	- (Oracle & SQL Server).
	
### Use case
- store relational datasets (RD BMS / OLTP)
- perform SQL queries, transactions.

## Aurora 

- Compatible API for PostgreSQL / MySQL.
	- Separation of storage and compute.
- ***Storage***
	- data is stored in 6 replicas., across 3 AZ.
	- Highly available, self-healing, auto-scaling.
- ***Compute***:
	- Custom endpoints for writer and reader DB instances.
- Same security / monitoring / maintenance features as RDS.
- Know the back-up & restore options for aurora.
- Aurora **Serverless**
	- for unpredictable / intermittent workloads, no capacity planning.
- Aurora Multi-Master
	- for continuouss writers failover (high write availability)
- Aurora Global
	- up to 16 Db Read Instances in each Region, <1 second storage replication
- Aurora Machine Learning
	- perform ML using **SageMaker** & comprehend on aurora.
- Aurora Database Cloning
	- new cluster from existing one, faster than restoring snapshot.

## ElastiCache
- Managed Redis / Memcached
- In-memory data store, sub-milisecond latency
- select an ElastiCache instance type (e.g., cache.m6g.large)
- Support for 
	- Clustering (Redis) 
	 - Multi-AZ
	 - Read Replicas (Sharding)
 - Sec through IAM, security Groups, KMS, Redis Auth
 - Back-up / Snapshot
 - Requires some application code changes to be **leveraged**.

### Use case
- Key-value store.
- Frequent reads.
- Less writes.
- Cache results for DB queries.
- Store session data for websites
- cannot use SQL.


## DynamoDB
- AWS proprietary tech
- managed serverless NoSQL database, millisecond latency.
- Capacity Modes:
	- **provisioned** capacity with optional auto-scaling.
	- **On-demand** capacity.
- Can replace ElasticCache as Key/Value store (storing session data for example using TTL feature)
- **Resilience.**
	- Highly Available.
	- Multi-AZ by **default**.
	- **Read** & **Writes** are **decoupled**
	- Transaction **capability**.
- DAX cluster for read cache.
	- Microsecond read latency.
- Sec, authentication, and authorization is done through **IAM**.
- Event Processing:
	- DynamoDB Streams to integrate with:
		- AWS Lambda
		- Kinesis Data Streams
- Global Table feature.
	- Read & writes from any region.
- Back-ups:
	- Automated back-ups up to 35 days with PITR(restore to new table).
	- On-demand back-ups.
- Import / Export directly to **S3**:
	- Exports don't use **RCU** within the PITR window.
	- Imports don't use **WCU**.

### Use cases
- Rapidly evolve schemas.
- Serverless applications development (small documents, 100s KBS).
- Distributed serverless cache.

## S3
- key / value store for objects
- Great for blob storage, bigger objects.
- **Architecture**:
	- Serverless.
	- Scale infinitely.
	- Max object size is **5TB**.
	- Versioning capability.
- Tiers + Lifecycle policies:
	- S3 Standard.
	- S3 Infrequent Access.
	- S3 Intelligent.
	- S3 Glacier Flexible Retrieval.
	- S3 Glacier Instant Retrieval.
	- S3 Glacier Deep Archive.
- Features:
	- Versioning.
	- Replication:
	- Batch operations:
		- S3 Batch: Batch operations.
		- S3 Inventory : List files,
	- **Encryption**:
		- SSE-KMS.
		- SSE-S3 (default).
		- SSE-C Client Side Encryption.
		- Client-side.
		- TLS in transit.
	- Replication.
	- MFA-Delete.
	- Access Logs
	- **Performance**:
		- Multi-part upload:
			- parallel chunks upload.
			- For files, > 5 GB.
		- S3 Transfer Acceleration:
			- to reduce latency for long-distance transfers of large objects. 
		- S3 Select
			- use SQL to perform server-side filtering.
			- 
### Use Cases
- static files.
- Key value store for big files.
- Website hosting.

# Document DB
- supports MongoDB
- Fully Managed
	- highly available with replication **across** 3-AZ
- auto grows in increments of 10 GBS up to 64 TB.

## Neptune
- Fully managed **graph** database
- a popular graph dataset would be **social network:**
	- **Users** have friends.
	- **Posts** have comments.
	- **Comments** have likes from users.
	- **Users** hared and like posts.
- Highly available across 3-AZ.
	- With up to 15 **read replicas**.
- Highly connected datasets.
-   Can store up to billions of relations.
- Great for knowledge graphs 
	- (e.g. Wikipedia).
	- Fraud detection.
	- **Recommendation** engines.
	- Social networking.

# Keyspaces for apache Cassandra

- Fully Managed.
- **Serverless**.
- Tables are replicated 3 times across multiple **AZ**.
- tables scales automatically.
	- Up / down based on the app traffic.
- Single digit **ms** latency 
	- 1000s of requests per second.
- Use Cassandra Query Language (CQL).
- Capacity Modes:
	- **provisioned** capacity with optional auto-scaling.
	- **On-demand** capacity.
- Features:
	- Encryption
	- back-up
	- Point-In-Time Recovery (PITR) up to 35 days.

## Use Cases
- store IoT Data.
- Time series Data.

# Quantum Ledger Database
- recording finical **transactions**.
- A ledger is a book **recording financial transactions**.
- Used to **review history of all the changes made to your application data** over time.
- Fully managed
	- serverless
	- high available
	- replications across 3 **AZ**
	- **immutable**
- **cryptographic** signature
- review **history** of **transactions**
- better performance than common ledger blockchain framings.
- Use **SQL** to gather data.
- 2-3x better performance than common ledger blockchain frameworks.
- No decentralization – central **database**.