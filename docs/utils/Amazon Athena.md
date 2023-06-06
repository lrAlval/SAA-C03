# Athena
- **serverless**.
- Uses SQL Language.
- Interactive query Service to analyze data in s3.
- Per only per queries run.
- **Process** logs.
- Ad hoc analysis.
- Expensive if data is not columnar.
- Store results back to [[S3]].
![[Pasted image 20230605223617.png]]

## Use case
- when you need to analyze data in S3 using **serverless**.
- **Commonly** used with [[QuickSight]].
- [[CloudTrail]] trails.
- [[ELB]] Logs
- query VPC Flow Logs.
- Business intel, analytics, reporting.
- Use [[Glue]] to convert data to **parquet** or **orc**.
- Partition data by path.
```
pathtoBucket/pathtotable
                        /partition_col_key
                        /partionen_col_key
```
- Use larger files

## Supported Data types
- **CSV**
- JSON
- ORC
- **Avro**
- **Parquet** (faster than CSV)

## Price
- 5 **Dollar** per **TB** scanned.

## Performance Improvement
- Use Columnar data for cost-savings (less scan)
	- Apache Parquet or ORC.
- Use Larger files > 128 Mb to minimize **overhead**.
- Use [[Glue]] to convert your data to Parquet or ORC.
- Compress data for smaller retrievals (bzip2, gzip,lz4,snappy, zlip, zstd).
- Partition datasets in S3 for easy querying on virtual columns:
	![[Pasted image 20230605223211.png]]

## Federated Query
- Query data from outside from [[S3]].
- One Lambda function per **Data Source Connector.**
- Use data source Connectors ([[Lambda]] function which connects to another service):
	- CloudWatch Logs.
	- DynamoDB.
	- RDS.

![[Pasted image 20230605223558.png]]