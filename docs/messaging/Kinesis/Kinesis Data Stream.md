>Scalable streaming service. It is designed to inject data from lots of devices or lots of applications.

## TL;DR
- ***Huge scale*** ***ingestion*** from multiple devices or services with multiple consumers.
- Store data for a **window of time**.
- **Rolling window** for multiple consumers.
- Designed for data ingestion, analytics, monitoring, app clicks.
- Retention between 1 day to 365 days.
- Data can't be deleted—immutability
- **Real-time**.
- **Fully managed**.

## Use cases
- Real-time analytics
- ***Huge scale Ingestion***
- Clickstream Analysis
- Fraud Detection
- IoT Data Ingestion and Processing
- Social Media Streaming and Analysis
- Gaming **Analytics**
- IoT Data Ingestion

## Limitations

- Once record age past the end of the rolling window, they are **deleted**.

## Features
- Many producers send data into a Kinesis Stream. 
	- Streams are the basic unit of Kinesis.
- The stream can scale from low to near **infinite data rates.**
- Highly **available** **public service** by design.
- Streams store a (default)24-hour—365 days (additional costs \$\$) moving window of data.
- Kinesis includes the storage costs within it for the amount of data that can be ingested during a **1-365 days. 
- Can have Many producers & consumers.
	- Multiple consumers can access data from that **moving** **window**.
	- Each consumer can have read data at different levels of granularity as long as it
	    - One might look at data points once per hour
	    - Another looks at data 1 per minute.
- Kinesis stream starts with **1** shard and **expands** as needed.
    - Each shard can have **1 MB**/s for ingestion. 
    - Each shard can have **2 MB**/s consumption.


## Kinesis Data Streams Detail
- shards which split data and computing power

### Record
- entry in kinesis.
- **Partition key** which targets the shard.
- Data blob (up to **1mb**).
- Producers can set **1mbs** and **1000msg** per sec per **SHARD**.

#### Consumer
- receives partition key, sequence number and blog.
- Throughput **2mbs** per sec shared for ***all consumers.***
- Enhanced Mode allows **2mb** per sec **per consumer.**
- Apps using SDK.
- [[Lambda]].
- Kinesis firehouse.
- Kinesis data analytics.

### Retention
- between 1 and 365 days.
- Can replay data.
- Immutability - can't delete messages.

### Security
- Encryption **at-rest** [[KMS]].
- Encryption **in-flight** **HTTPs**
- can also use **client side** encryption.
- Control access / authorization using [[IAM]] policies
- [[docs/networks/VPC]] endpoint for access from [[docs/networks/VPC]]
- Monitor API calls using [[CloudTrail]]

### Modes

#### Provisioned Mode 
- choose number of **shards**, scale **manually**.
- Each **shard** gets 1 MB/s ***IN*** (or **1k records** per second)
- Each shard gets 2 MB/s ***OUT*** (classic or enhanced fan-out consumer)
- Pay per **shard** per hour.

#### On demand
- No need to provision or manage the capacity.
- Default capacity provisioned (**4mbs IN or 4k records per second**).
- Scales on **throughput** **peak** observed within the last **30 days**
- Pay per **stream per hour** & data **IN/OUT** per GB.
