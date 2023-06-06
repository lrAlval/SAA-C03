>Extract, transform & load streams into multiple AWS services 

## TL;DR
- ***NEAR-REALTIME Delivery - (60 secs)***.
- Deliveries Streams into supported **destinations** in **batches**.
- Allows delivery / transformation of streams to supported **destinations**.
	- Any HTTP endpoints
	- ElasticSearch
	- [[Amazon Redshift]]
	- [[OpenSearch]]
	- Splunk
	- Datadog

## Use cases
- Data Lake Ingestion.
- Log and Event Data Archival.
- Near Real-time Data Transformation.
- Near Real-time Analytics.
- Data Replication and Backup.
- Clickstream and User Behavior Tracking.
- IoT Data Processing.


## Common Scenarios
- Permanent storage of stream data in S3.
- Transform and store data in different format.
- Load Stream into one of the supported destinations.

## Features
- Support transformation of data on the fly [[Lambda]]
- Auto Scaling.
- Fully serverless.
- Resilient.
- **Billing – volume** through firehose.

## Limitations
- only one consumer at the time **per stream**.

## Performance
- Near **real-time** delivery
- batch buffer size 1Mb or 60 seconds.

### Cost
- pay per **data** send
- near real time (60 sec minimum)

## Destinations
- Destination Bucket -  [[S3]]
- Any HTTP endpoints
- ElasticSearch
- [[Amazon Redshift]]
- [[OpenSearch]]
- Splunk
- Datadog
- New Relic
- Datadog
- MongoDb
