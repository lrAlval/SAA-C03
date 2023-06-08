# Could Trail for Cloud Watch
- ***Global Service***.
- Tracks and logs API requests within the AWS account.
- Used for governance, compliance, operational auditing and risk auditing.
- Can be used to trigger events on AWS [[EventBride]]
- **enabled** by default.
- A trail can be one or all regions.
- Stored for ***90 days***, default
	- for events older than 90 days , should use [[Amazon Athena]].
- Transfer to [[S3]] for longer retention.
- Trail names need to be globally unique.
- US-east-1 → default region for global services.
- IAM, STS, CloudFront → Global Service events.
- **NOT REAL-TIME – there is a delay – 15 mins.

## Management Events
- Configuring Security. 
- Enabled by **default**.
- Read and write **event** types.

## Data Events
- by default not logged.
	- e.g., S3 object level activity.
- Read and Write event types.

## Cloud Trail Insights Events:
- **ML**.
- Detect unusual activity in write events.
- Send to [[S3]], [[EventBride]] and cloud trail console.

## Security
- logs are encrypted by default using [[KMS]] AWS Managed keys.