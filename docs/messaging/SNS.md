![[Pasted image 20221101163353.png]]
# Amazon Simple Notification Service

## TLDR
>Message queue with a subscriber model. It can send the same message to a lot of different services at once. Scales good but not indefinitely.

## Features
- subscriber async model
- **Pub** / **sub** model.
- One producer multiple consumers/**subscribers**
- up to 12 **million** subscriptions per topic
- up to 100k topics.

## Sources
- [[CloudWatch]] alarms
- [[ASG]] Notifications
- AWS Budgets [[AWSBilling]]
- [[Lambda]]
- [[DynamoDB]]
- [[Cloudformation]]

## Targets
- [[Kinesis]] Data Firehouse
- [[docs/messaging/SQS]]
- [[Lambda]]
- HTTP
- E-Mail
- push
- SMS

## Topic Publish
- create a **topic**
- add subscriptions to topic
- publish to the topic

## Direct Publish
- for mobile apps
- create platform app
- create platform endpoint
- publish to endpoint
- Google GCM
- Apple **APNS**.
- Amazon ADM.

## Security
- HTTPS by default
- at rest using [[KMS]]
- client side optional
- [[IAM]] for access control
- SNS access policies
	- resource based for **cross account** or other services.

## FIFO
- same as [[docs/messaging/SQS]] FIFO
- ordering by message group id (all message in the same group are ordered)
- deduplication using deduplication Id or content based deduplication.
- Only SQS FIFO can be a subscriber.

##

## Filtering
- JSON policies on a subscriber 
- will only receive msg which match the filter
- can be used with fan out to split SNS messages to multiple dedicated [[docs/messaging/SQS]] queues

## Patterns
- SNS + SQS
![[Pasted image 20230601174933.png]]

- S3 Events to multiple queues
![[Pasted image 20230601175140.png]]

- SNS → Kinesis → S3
![[Pasted image 20230601175234.png]]
- SNS FIFO → SQS FIFO 
![[Pasted image 20230601175448.png]]

- SNS Message Filtering → SQS Queue

![[Pasted image 20230601175631.png]]