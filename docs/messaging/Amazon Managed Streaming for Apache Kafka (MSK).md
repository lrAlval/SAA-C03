# Amazon Managed Streaming
- alternative to Kinesis
- Fully managed Apache Kafka on AWS
- cluster
## MSK Serverless
- no provisioning
- automatic scaling

## Difference to Kinesis
- Kinesis 1 MB limit per MSG, MSK 10 MB.
- kinesis shard, Kafka topics.
- Kafka doesn't enforce SSL.
- Kafka can only add **partitions** to a topic.

## Consumers
- Apps (EC2, ECs, EKS)
- Kinesis Data Analytics
- GLUE
- Lambda