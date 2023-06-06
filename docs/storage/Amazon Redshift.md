# Features
- **petabyte** Scale Data warehouse
- online analytical processing (**OLAP**)
	- analytics and data **warehousing**.
	- 10x better performance than other data warehouses
	- scale to PB's of data.
- Columnar storage of data & **parallel** query engine.
- Pay as you go. 
- Large scale data storage and analysis.

## Drawbacks
- data must first be loaded into Redshift.

## Use case
- intense data warehousing with many queries.


## Loading Data
- [[Kinesis Data Firehose]]
- S3 using COPY command.
- ***EC2 Instance***.

## Resilience
- Multi-AZ for some clusters.
- For single AZ – use snapshots.
	- Snapshots are point-in-time backups stored internally in S3.
		- Snapshots are incremental (only what has changed is saved).
		- You can restore a snapshot into a new **cluster**.
			- Can be configured to be copy snapshots into another **AWS Region**.
			- Automated or Manual (snapshot is retained until you delete it): 
			- every 8 hours
			- every 5 GB
			- or on schedule.
		![[Pasted image 20230605225951.png]]

## Architecture
- ***Leader node***: for query planning, results aggregation.
- ***Compute node***: for performing the queries, to send results to leader.
- You provision the node size in advance.
- You can use reserved instances for cost savings.

## Integration
- [[QuickSight]]
- Tableau.

## Vs Athena 
- faster queries, joins, aggregations thanks to indexes.

## Spectrum
- attach **S3** without the data being **transferred** to Redshift
![[Pasted image 20230605230352.png]]