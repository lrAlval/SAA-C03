![[Pasted image 20221101210837.png]]
# Amazon Aurora

## TLDR
AWS Created custom DB tech, very high performan. Useful for global and serverless relational database applications.

## Features
- not open source
- Failover is instantaneous [[### High Availability (HA) |HA Native]]
- MySQL and Postgres
- global
- self-healing
- [[docs/essentials/Resilience concepts#Fault-Tolerance (FT) 💰|Fault Tolerant]]
- storage automatically grows in increments of **10Gb** up to 128 Tb
- autoscaling up to 64 TB per instance
- is a **cluster**
- **multi AZ**
- each **AZ** has a copy of the cluster.
- 5x faster than **MySQL**.
- 3x fast than **Postgres**.
- up to **15** replicas.
- faster **replication**.
- 20% more cost than [[RDS]]
- automated patching with **zero downtime**
- **backtrack** restore to any point in time **without** **backups** (up to **72** hours)

#### High Availability & Read Scaling
- 6 copies of your data across 3 **AZ**
	- 4 copies out of 6 needed for writes
	- 3 copies out of 6 needed for **reads**
	- self-healing with peer-to-peer replication.
	- Storage is **striped** across **100s** of volumes.
- One aurora **instance** takes **writes** (master)
- automated **failover** for master in **less** than **30 seconds.**
- Master + up to **15** read replicas to serve **reads**
- support for **cross** **region** **replication**.
	- Cross region read replicas:
	- useful for [[docs/essentials/Resilience concepts#Disaster Recovery (DR) ☠️|Disaster Recovery]]
	- simple to use
	
![[Pasted image 20230523172247.png]]

#### Aurora Db Cluster
- Reads replicas are behind **auto**-**scaling**
![[Pasted image 20230523172503.png]]


## Primary DB
- **read** and **write**
- only one per **cluster**
- if **fails** a **replica** **will be promoted**

## Aurora Replica
- same **storage** as primary
- **multiple** per AZ possible
- **only read**
- reader **endpoint** does load **balancing**
- can enable **replica** **autoscaling**

## Custom Endpoints
- subset of **aurora** instances as custom endpoint
- once a custom endpoint is enabled, reader endpoints no longer works.
- (e.g., larger **instance type** for analytical queries)

## Aurora Serverless
- automated db **instantiation** and **autoscaling**
- useful for **infrequent**, **unpredictable** and **intermittent** workloads
- no capacity planning needed.
- Pay **per second**
- client talks to aurora proxy fleet.

![[Pasted image 20230523180223.png]]

## Aurora Multi-master
- use for **immediate** **failover** ([[docs/essentials/Resilience concepts#High Availability (HA) **🏷️**|High Availability]])
- all nodes are **R/W**  vs. promoting a **RR** (*Read Replica*) as a new **master**, 
- there is no **master**
- **replication** between all nodes

![[Pasted image 20230523180729.png]]

## Global Aurora Database
- 1 primary **region** for **R/W**
- up to 5 **secondary** read regions
- up to **16 read replicas** per **secondary read** region.
- **Less** than 1 second for **replication** **across region**
	- helps for decreasing latency **worldwide**.
- Promoting another region for (**DR**) has an [[docs/essentials/RPO & RTO#Recovery Time Objective (RTO)|RTO]] of < 1 minute.

![[Pasted image 20230523181712.png]]

## Aurora Machine Learning
- ML based predications to your apps via **SQL**

### Use cases
- Fraud Detection
- add targeting
- Sentiment analysis (AWS comprehend)
- product recommendations

### Services
- [[SageMaker]]
- [[Amazon Comprehend]]

## Backups

### Automated 
- 1 to 35 days (**cannot** be disabled)
- point in time recovery in that timeframe

### Manual
- triggered by user
- keep as long as user wants

### Restore
- into **new database**

### Cloning
- create a new aurora cluster from an existing one
- faster than **snapshot** & **restore**
- **cost-effective**
- useful to **create** **staging**
