> Real-time data processing service.

## TL;DR
- **Real time processing** of data using **SQL**
- Ingests from [[Kinesis Data Stream]] or [[Kinesis Data Firehose]]
- Destinations / outputs:
	- [[Kinesis Data Firehose]] (S3,Redshift, ElasticSearch, OpenSearch & Splunk)
	- [[Lambda]]
	- [[Kinesis Data Stream]]

## Use cases
- Streaming data **needed** real-time processing
- time-series analytics
	- **elections / e-sports**
- Real-time dashboards
	- **leaderboards** for games
- Real-time metrics
	- **Security** & **Response** teams

## Features
- Fully managed, no servers to provision
- Automatic scaling
- Pay for actual consumption rate

## Data Analytics for Apache SQL
> Streaming data **needed** real-time SQL processing.

- Serverless.
- Auto Scaling.
- Pay per consumption rate.
- Inputs:
	- [[Kinesis Data Stream]] or [[Kinesis Data Firehose]].
- Outputs: 
	- [[Kinesis Data Stream]] or [[Kinesis Data Firehose]]
- Can enrich data from [[S3]]
- send against to another Kinesis Stream or Firehouse
- Use cases
	- Time-series analytics using SQL.
	- Real-time dashboards using SQL
	- Real-time metrics using SQL.

## Data Analytics for Apache Flink
- Use Flink (Java, Scala, or SQL) to process or **analyze** streaming data
- application backups (**implemented** as checkpoints and snapshots)
- Run any Apache Flink app on a managed cluster on **AWS**.
	- Provision compute resources.
	- Parallel computation.
	- Automatic scaling.
- Use any Apache Flink programming **features**.
- Inputs: [[Kinesis Data Stream]] or [[Amazon Managed Streaming for Apache Kafka (MSK)]]

## Usage
- more powerful queries
- run complex queries