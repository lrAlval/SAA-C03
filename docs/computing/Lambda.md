![[Pasted image 20221030233208.png]]
# AWS Lambda
>AWS Lambda means you don't care about any infrastructure, you just upload a function to AWS. You can then use that function from other services like  [[APIGateway]], [[SNS]] or even [[CLI]]. You upload Lambda code as a zip.


## TLDR
- Limited by time – **short executions**
- Scaling is automated.
- Apps must be **state-less.**
	- Brand-new invocation, brand-new env.
- vCPU is allocated **indirectly**  & scales with the memory ***allocated***.
	- 128 (default) – 10240 MB
- /**tmp** storage (512Mb-10240Mb)
- Max run time (**15** mins)
- Lambda functions 
- By default only public traffic
	
## Features
- Run **code** **serverless**
- Pay per compute time
- scaling is automated
- No charge if not running
- Operates from AWS owned [[VPC]]
- By default **only public traffic**.
- You can enable function [[VPC]] access if you need private resources from your [[VPC]]
- Scale up based on request amount
- Can set custom function timeout
- Can be packaged and deployed as container images

#### Key Considerations

- Max execution run time (900s – 15 mins)
- Assume each execution gets a new runtime environment.
- Use the execution role which is assumed when needed.
- Always load data from other services from public APIs or S3.
- Store data to other services (e.g., **S3**).
- 1M free requests and 400,000 GB-seconds of compute per month.

## Drawbacks
- Limited by time ***SHORT EXECUTIONS***
- if you need both private and public resources, you will have to enable [[VPC]] access and use a  [[NAT]]  gateway to access the internet

## Use cases
- Serverless applications ([[S3]], [[APIGateway]], Lambda)
- File Processing ([[S3]],S3 Events, Lambda)
- Database Triggers (DynamoDB, DynamoDB Streams, Lambda)
- Serverless CRON ([[EventBride]]/[[CloudWatch]] Events + Lambda)
- Real-time Stream Data Processing (Kinesis + Lambda)

## Logs
- uses [[CloudWatch]], CloudWatch Logs & X-Ray
- logs from Lambda executions - CloudWatch Logs
- Metrics – invocation successes/failures, retries, latency stored in [[CloudWatch]].
- Lambda can be integrated with x-ray for distributed tracing.
- CloudWatch Logs requires ***permissions via Execution Role***


## Some Integrations

![[Pasted image 20230604203039.png]]

## Examples

### Serverless Thumbnail creation

![[Pasted image 20230604203258.png]]

### Serverless CRON Job

![[Pasted image 20230604203324.png]]


## Invocation
- **Synchronous invocation.**
	- Human directly  or indirectly invoking the lambda.
	- Result (success or failure)have to be handled within the client.
	- Errors or Retries have to be handled within the client.
- **Asynchronous invocation.**
	- Typically, used when **AWS** services invoke lambda functions.
	- Lambda function needs to **idempotent**.
		- ***Reprocessing*** a result should have the same end state.
	- Events can be sent to **DLQ** after repeated **failed** processing.
	- Lambda supports destinations where successful or failed events can be sent:
		- [[SQS]]
		- [[SNS]]
		- [[Lambda]]
		- [[EventBride]]
- **Event Source mappings.**
	- Typically used on streams or queues which don't support event integration to invoke **Lambda**
		- [[Kinesis Data Stream]].
		- [[DynamoDB]] Streams.
		- [[SQS]].
	- Pull events in batches.
	- Permissions from the lambda execution role are used to access each resource when using **event source mappings**.

## Versions
- a version is the code + the config of the lambda
- it's immutable.
	- It never changes once published & it has its own ARN
- Aliases (DEV, STAGE, PROD) point at a version – can be *changed**

## Startup
- per invocation, a new **execution context** is created
- can use ***Provisioned concurrency*** to keep X contexts warm and ready to use
	- improving start speeds.

## Security

- [[IAM]] roles control permissions **lambda** **function** receives.
- Lambda has **resource policy.**
	- What **services** and accounts CAN **INVOKE** **lambda** functions?

### Lambda authorizer
- Send additional info based of **bearer** token or request context
- Is useful because you can skip having too lookup users inside of your function  (you pass the user data)
- Don't pass credentials! (Though you could)

## Compute Power
- Relative to memory allocation, which can be manually set

## Lambda Layer
- Zip archive which contains libraries, custom runtime and other dependencies
- A single function can use up to 5 **layers**.
- Can use self created layers or already published ones
- Unzipped size cannot exceed 250mb for a function and all layers which it depends on

## Container Image
- If using an image, the image must implement the  [[Lambda]] runtime API.
- Docker in Lambda is anti **pattern**.
- [[ECS]] and **Fargate** is preferred for running arbitrary docker images (without Lambda runtime API embedded in the image).

## Price
- ***Pay per calls:***
	- First 1 million are **free**.
	- 0.20 cent per one million request after
- Pay per ***duration(in increments of 1 ms)***:
	- 400000 GB-Seconds per month free
	- Price scales up after that depending on GB seconds (more will be cheaper per GB second)


## Limits Per Region

### Memory 
- 128 MB to 10 GB (1mb increments)

### Max Exec Time
- 900 seconds/ 15 mins

### ENV vars
- 4kb for all vars together

### Disk
- 512 MB to 10 GB 

### Concurrency
- **1000** but can be increased

### Deployment

#### Zip Size
- 50 MB

#### Uncompressed With Dependencies
- **250** MB

#### TMP
- can use /tmp to load other files after/on startup
	- 512 MB to 10Gb

