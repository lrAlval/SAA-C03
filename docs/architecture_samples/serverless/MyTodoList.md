
>high overview requirements:

- Expose as REST API with HTTPS.
- Serverless architecture.
- Users should be able to directly interact with their own folder in S3.
- Users should authenticate through a managed serverless service.
- The users can write and read to-dos, but they mostly read them.
- The database should scale and have some high read throughput.

## Solution
- Serverless REST API: HTTPS  
	- API Gateway
	- Lambda
	- DynamoDB
- Cognito to generate temp credentials with **STS** to access S3 bucket with restricted policy.
- App users can directly access AWS resources this way.
	- Pattern can be applied to **DynamoDB**, **Lambda**.
- Caching the  reads on **DynamoDB** using **DAX**.
- Caching the REST request at the **API Gateway** level.

#### Giving users access to S3
![[Pasted image 20230605172205.png]]

#### High read throughput, static data
> adding DAX caching layer to increase performance since most queries are reads.

![[Pasted image 20230605172455.png]]

#### can also cache some responses in the API Gateway

![[Pasted image 20230605172549.png]]