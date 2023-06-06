![[Pasted image 20221101125233.png]]
# Simple Queue Service

## TLDR
>AWS standard queue service. Has ton of features like **FIFO** and **multi** **consumer**. Scales indefinitely.

## Features
- AWB managed
- async systems
- decouple
- message delay up to 15 min
- unlimited **throughput** 
- unlimited number of messages
- default retention **4** days, max **14** days
- max size **256kbs**
- dynamically add **concurrency**/ read **throughput**
- track ACK/Fail 
- set visibility timeout for ACK/Fail
- scale transparently
- buffer **requests**
- can have out of **order** messages (  best effort ordering)
- can have **duplicate** messages
	-  [[docs/essentials/Message Delivery Reliability#**At-least-once semantics**|At east once]] Delivery

## Message Delivery Reliability
-  [[docs/essentials/Message Delivery Reliability#**At-least-once semantics**|At east once]] Delivery
- best-effort message ordering.

## Performance
- low latency (< 10 **ms**)
- SQS Standard: unlimited **throughput** 

## Producers
- needs to use SDK/API

## Consumers
- [[EC2]] instances, [[Lambda]] 
- Polls queue, receives up to 10 **msg** at a time
- after processing use SDK/API to send delete msg command to [[docs/messaging/SQS]]

## Types
- cannot convert between types, resource needs to be recreated

### Standard
- max **throughput**.
- Best **effort** ordering.
- **At least once delivery**.

### FIFO
- first in first out
- queue name needs to end with .FIFO
- delivered **exactly** once
- no **duplicates**.
- max **3k** per second with batching
- max **300** per second without batching

## Security
- **In-flight** encryption using HTTPS API 
- **at rest** encryption with [[KMS]] keys
	- SSE-SQS: SQS service creates, manages and uses the key.
	- SSE-**KMS**: key rotation by [[KMS]]
- **Client side** encryption also possible
	- if client wants to perform encryption/decryption **itself**.
- [[IAM]] to control access to queue.
- **SQS** Access policies.

### SQS Access policies
- **resource** based permissions
- **cross**-account
- other services **without** [[IAM]] role

## Visibility Timeout
- default 30 sec, min 0 sec , max 12 hours
- after polled msg becomes invisible
- message visibility timeout window is 30 seconds.
	- Can use **ChangeMessageVisibility** API to increase time.
- Set to process time to stop being processed twice.
- If process time takes longer can use **SQS** API to increase visibility timeout for this message.

## Long Poling
- Queue gets polled for longer time to wait if queue is empty.
- Decrease the number of **API** calls.
- Between **1** and **20** seconds
- can be configured at queue level or in **API** request.
- Useful when needed to reduce API calls & decrease latency.

## Practical Patterns 

- useful for decoupling
- sudden spike load

![[Pasted image 20230601171601.png]]

![[Pasted image 20230601173802.png]]

![[Pasted image 20230601174007.png]]
