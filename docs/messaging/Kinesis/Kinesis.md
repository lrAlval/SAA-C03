![[Pasted image 20221101120425.png]]
# Kinesis

## TLDR
>Kinesis is a set of services for streaming real time or next to real time data in AWS. It's generally more expensive and more difficult to set up than [[docs/messaging/SQS]] but offers more features and higher performance.

## Features
- **region** scoped
- real **time** data streaming service
- gigabytes of data per second
- **100ks** of sources
- 2MBs/shard default shared between all consumers of kinesis stream
- use enhanced fan out to support multiple consumers, each consumer gets the 2mbs/shard
- 1mbs input per shard 
- shards need to be provisioned ahead of time
- consume records up to 7 days later
- multi applications consume the same stream
- keep order of records
- routing related records to the same consumer

## Components

- ***Kinesis Data Streams***: capture, process & store data streams.
- ***Kinesis Data Firehose:*** load data streams into AWS data stores.
- ***Kinesis Data Analytics***: analyze data streams with SQL or **Apache Flink**.
- ***Kinesis Video Streams***: capture, process and store video streams.

## Kinesis Data Streams Detail
- shards which split data and computing power

### Record
- **entry** in kinesis
- uses Sharding
- **partition key which** targets the shard
- data blob (up to 1mb)
- Producers can set 1mbs and 1000msg per sec per SHARD

#### Consumer
- receives partition key, sequence number and blog.
- Throughput 2mbs per sec shared for all consumers.
- Enhances 2mb per sec per consumer.
- Apps using SDK.
- [[Lambda]].
- Kinesis firehouse.
- Kinesis data analytics.

### Retention
- between 1 and 365 days.
- Can replay data.
- Immutability

### Security
- [[KMS]] at rest
- **HTTPs in flight**
- [[IAM]] for access
- can also use client side encryption
- [[docs/networks/VPC]] endpoint for access from [[docs/networks/VPC]]
- monitor with [[CloudTrail]]

### Producers
- Clients
- Apps
- SDK
- Kinesis Agent
- AWS IOT
- [[CloudWatch]] logs and events
- kinesis data streams

### Targets
- [[S3]]
- [[Amazon Redshift]]
- Elasticsearch
- Splunk
- custom HTTP endpoints

## Data Ordering in SQS vs. Kinesis
>kinesis your producers need to use the same partition/shard key for related data

- in [[docs/messaging/SQS]] there is no ordering
- in [[docs/messaging/SQS]] FIFO there is only one consumer and order stays the same
- in [[docs/messaging/SQS]] FIFO queue if you want to send related data to different consumers you use a **group** id, which works then similar to kinesis

### [[docs/messaging/SQS|SQS]] VS [[SNS]] VS [[Kinesis]]

#### [[docs/messaging/SQS||SQS]] 
- pull data then delete message via API call from consumer
- Message is processed by exactly once consumer (hopefully)
- as many workers as you want
- scales indefinitely
- need FIFO for order

#### [[SNS]]
- push same data to multiple subscribers
- data is not persistent
- fan out to combine with SQS

#### Kinesis
- standard 2mb per shard pull data
- consumers can consume data concurrently
- enhanced fan ut 2mb per shard per consumer, push data
- limited amount of consumers (by shard)
- replay data
- ment for real time big data
- ordering at shard level
- data will expire after x days