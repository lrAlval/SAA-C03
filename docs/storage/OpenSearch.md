# OpenSearch
- ex **Elasticsearch**.
- Can be used for search.
- Can be used for analytic queries.
- Requires a cluster of instances.
- Does not natively support **SQL**.
	- Can be enabled via a **plugin**.
- Integrates good with kinesis and lambda.
- Comes with OpenSearch Dashboards (visualization).
- **Security**:
	-  Cognito.
	 - IAM.
	 - KMS Encryption.
	 - TLS.
- Two modes:
	- managed cluster.
	- Serverless cluster.

## OpenSearch Patterns
- DynamoDB

![[Pasted image 20230605230936.png]]

- CloudWatch Logs
	![[Pasted image 20230605231110.png]]
- Kinesis Data Streams & Kinesis Data Firehose
![[Pasted image 20230605231136.png]]