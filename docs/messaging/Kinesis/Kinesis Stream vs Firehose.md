- Kinesis Streams to capture data in real time, and ingest at scale
- Firehouse to load streaming into AWS data stores
- **Firehouse** is not real time.
- **Firehouse** has close ended consumer options
- **Firehouse** can have only one consumer at the time.

## Kinesis Data Streams
-  ***Huge scale*** ***ingestion*** from multiple devices or services.
- Multiple consumers simultaneously.
- Streaming service for ingest at scale.
- Write custom code (producer/consumer).
- Real-time (200 **MS**).
- Manage scaling (shard splitting / merging).
- Data Storage for 1 to 365 days.
- Supports replay capability.

## Kinesis Data firehose
- **Load Streams** into destinations.
- **NEAR REAL-TIME** (60 secs batches)
- Only support 1 **consumer** at the time.
- Load streaming data into:
	- S3
	- Redshift
	- OpenSearch
	- ElasticSearch
- Fully Managed
- Automatic scaling.
- No data storage.
- Doesn't support replay capability.