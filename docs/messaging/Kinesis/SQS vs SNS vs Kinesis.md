#### [[docs/messaging/SQS||SQS]] 
- Pull model.
- Fully **managed**.
- Pull data then **delete** message via API call from **consumer**
- message is processed by **exactly** **once** consumer (hopefully)
- as many workers-consumers as you want
- Individual message delay **capability**.
- **Scales** **indefinitely**
- need FIFO for order.

#### [[SNS]]
- **pub/sub** model.
- Fully **Managed**
- Push same data to multiple subscribers.
- Data is not persistent.
- Fan out to combine with **SQS**.

#### Kinesis
- 
- **Standard** 2mb per **shard** pull data
- **Enhanced-fan** out: **push** data.
	- 2 MB per shard per consumer.
- **Replay** data.
- Meant for real-time big data, analytics and **ETL**.
- Ordering at shard **level**.
- Data expires after (1-365 days).
- Consumers can consume data **concurrently**
- enhanced fan at 2mb per shard per consumer, push data
- limited amount of **consumers** (by shard)