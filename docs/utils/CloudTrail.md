# Could Trail for Cloud Watch
- tracks and logs api requests within the aws account
- used for governance, complicance, operational auditing and risk auditing
- can be used to trigger events on AWS [[EventBride]]
- enabled by default
- a trail can be one or all regions.
- stored for 90 days default
- tranfer to [[S3]] for longer retention 
- trail names need to be globally unique.
- US-east-1 => default region for global services.
- IAM, STS, CloudFront => Global Service events.
- NOT REALTIME - there is a delay - 15 mins 

## Management Events
- Configuring Security 
- ...
- enabled by default
- read and write event types
## Data Events
- by default no logged
- e.g. S3 object level activity
- read and write event types

## CloudTrail Insights Events:
- ML
- Detect unusal activity in write events
- send to [[S3]] , [[EventBride]] and cloudtrail console

## Security
- logs are encrypted by default using [[KMS]] AWS Manged keys