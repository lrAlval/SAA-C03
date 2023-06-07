![[Pasted image 20221101205129.png]]
>Central **message** service with the most amount of **targets**. Is used by AWS behind the scenes a lot.

## Features
- Formerly known as ***CloudWatch Events***.
- Schedule (cron jobs).
	- Schedule scripts.
- Event pattern (email when root user logs in).
	- React to events from another services.
- Trigger Lambda functions, send SQS/SNS messages.
- JSON format.
- Can archive events.
- Replay archived events.
- Event JSON is typed, can be nice for custom code/lambda.

## Sources
- [[EC2]].
- Code Build.
- [[S3]].
- [[TrustedAdvisor]].
- [[CloudTrail]] (any API call).
- schedule (**cron**).
- 3rd Party.


## Targets
- [[Lambda]]
- [[Batch]].
- [[ECS]].
- [[docs/messaging/SQS]].
- [[SNS]].
- [[StepFunction]].
- Pipelines.
- [[Kinesis]]
- [[SSM]]
- 3rd Party
![[Pasted image 20230606222530.png]]


## Event Buses
- supports **resource** based policies.
	- Allow / deny events from another AWS **account**.
	- Aggregate all events from your AWS Organization in a single account or  AWS region.
![[Pasted image 20230606231834.png]]
- Can allow events from **other** **accounts**.
- Can ***replay archived events***.
- Can **archive events** (all / **filter**) sent to an event bus
	- indefinitely or set period.
	
![[Pasted image 20230606222935.png]]

## Schema Registry
- schemas from events auto generated.
- Schemas can be versioned in registry.
- 
![[Pasted image 20230606231641.png]]




### Default
- AWS Services.

### Partner Event bus
- supported 3rd party events.
- https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-saas.html
	- Datadog.
	- Zendesk.
	- Auth0.

### Custom Event Bus
- for custom apps.
