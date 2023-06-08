![[Pasted image 20221101162633.png]]
> Central service for all logs and metrics in AWS.

## TLDR
Central service for all logs and metrics in AWS.

## Features
- can set up alarms.
- Can stop, **terminate**, reboot and recover [[EC2]] instances.
- Can trigger [[Lambda]] or [[EventBride]].

## CloudWatch Metrics
- Metrics for every **service** in AWS.
- Bucket  by namespaces.
- Up to **30** dimensions per metric.
- A metric can has up to **10** attributes.
- Metrics can have timestamps.
- Can create dashboard.
- Can create custom metrics.

#### Metrics NOT Collected
-   **Memory** utilization
-   Disk swap utilization
-   Disk space utilization
-   Page file utilization
-   **Log** collection
-   If you need the above information, then you can **retrieve** it **via** the official **CloudWatch agent**, or you can create a **custom metric** and send the **data** on your own via a **custom script**.

### CloudWatch's metrics streams
- continually stream CloudWatch metrics to:
	- [[Kinesis]] **Firehouse**.
	- 3rd party providers.
		- Dynatrace.
		- New Relic
		- Splunk.
		- Sumo Logic.
	- Option to filter metrics, to just send a subset.

## CloudWatch Logs
- Log **groups** (**application** name).
- Log **steam** (log files, instances within on app, containers).
- Can define log expiration days (1 day to 10 years).
- Logs are **encrypted by default.**
- Can set up KMS-based encryption with your own keys.

## Sources

![[Pasted image 20230606194907.png]]

### Targets To Send Logs To
- [[S3]] .
- [[Kinesis]] data streams.
- [[Kinesis]] data firehouse.
- [[Lambda]].
- Elasticsearch.
- OpenSearch.

### How to send Logs
- SDK.
- CloudWatch Logs agent.
- CloudWatch unified agent.
- [[ElasticBeanstalk]], collection of logs from application.
- [[ECS]] collection from containers.
- AWS [[Lambda]] collection from function logs.
- [[VPC]] flow logs.
- [[APIGateway]].
- [[CloudTrail]] based on filter.
- [[Route53]] DNS requests.

### Filter 
- look for IP.
- look for string.
- Can trigger CloudWatch alarms.

### Insights
- query logs for dashboard
- Query engine, ***NOT Real-time***.
- Can query multiple  log groups in different AWS accounts.
- Auto discovers fields from AWS services and JSON log events.

![[Pasted image 20230606195032.png]]

![[Pasted image 20230606195237.png]]

#### CloudWatch Container Insights
- collect and **aggregate** logs from containers.
- [[ECS]].
- [[EKS]].
- Kubernetes platforms on EC2.
- Fargate (both for [[ECS]] and [[EKS]].
- Used **containerized** version of the **container** **agent**.

#### CloudWatch Lambda Insights
- metrics for [[Lambda]] functions
	- CPU time.
	- Memory.
	- Disk.
	- Network.
- It is provided via [[Lambda]] layer.
- Collets, aggregates & summarizes diagnostic info.
	- Cold starts.
	- Lambda worker shutdowns.

#### Contributor Insights
- Top N Contributors to Network traffic.
- Identify **bad** hosts.
- Works for any AWS-generated logs (VPC,DNS, etc..)
- Identify the heaviest **network** **users**.
![[Pasted image 20230606233742.png]]

#### CloudWatch Application Insights
- automated dashboard with monitored applications
- Support only select tech stack on ec2 (java, IIS, databases)
- can use additional resources ([[RDS]], [[S3]], [[SNS]] ...)
- Powered by Sage maker
- reduce time to troubleshoot
- alters and findings are sent to [[EventBride]] and [[SSM]] Ops Center.

### Export
-  to s3 up to 12 hours.
- API call is “**CreateExportTask**”.
- Use log subscriptions for real time.

### Log subscriptions
- Use a filter.
- Sent destination:
	- [[Kinesis Data Stream]]
	- [[Kinesis Data Firehose]]
	- [[Lambda]]


![[Pasted image 20230606200225.png]]

### Multi account
- use one central kinesis and subscriptions.

## CloudWatch Agent
- software on ec2.
- Needs correct permission.

### CloudWatch Logs Agent
- old version 
- only send to [[CloudWatch]] logs

### CloudWatch Unified Agent
- more granular metrics than old agent.
- Collects system level metrics such as RAM processes etc.
- out-of-the box metrics for EC2
	- Disk.
	- CPU.
	- network (high level).
- Collect logs to send to [[CloudWatch]] logs.
- Configuration via [[SSMParameterStore]].

### Metrics
- **CPU** 
	- active.
	- Guest.
	- Idle.
	- System.
	- User.
	- Steal.
- Disk Metrics
	- free.
	- Used.
	- Total.
- Disk IO
	- writes.
	- Reads.
	- Bytes.
	- Iops.
- Netstat:
	- Number of TCP connections.
	- Number of UDP connections.
	- Net packets.
	- Bytes.
- Processes
	- total.
	- Dead.
	- Bloqued.
	- Idle.
	- Running.
	- Sleep.
- Swap Space:
	- free.
	- Used.
	- Used %.

## CloudWatch Alarms
- trigger notifications from any **metric** or filter.

### Stages
- OK.
- Insufficient Data.
- Alarm.

### Period
- length of time to evaluate the metric.

### Targets
- [[EC2]] instance actions (stop, terminate, reboot, recover).
- Trigger [[ASG]].
- [[SNS]].

### Composite Alarms
- multiple alarms combined (multi metric alarm).
- And or conditions.

### [[EC2]] Instance recovery
- Status Check.
- start recovery (move host but keep **IPS**, metadata and placement groups).