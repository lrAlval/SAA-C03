# Systems Manager Parameter Store
- secure storage for configuration and secrets.
- Optional encryption using [[KMS]].
- Serverless.
- Easy SDK.
- Version tracking.
- Configuration management using [[IAM]] and path.
- Notifications with CloudWatch events
- [[Cloudformation]] support.

## Path
- prod/db/pw e.g.

## Cost

### Standard
- Storage up to ***10k*** parameter free.
- Max size ***4k***.
- No policies.
- Higher **throughput** for **API** (up to 1k per sec) 
	- cost 5 cent per 10k calls.

### Advances
- Storage up to ***100k***.
- Max size ***8kb***.
- ***Policies*** can be used.
- ***Throughput*** the same as standard.
	- 0.05 cent per parameter per month.

## Policies
- assign ***TTL*** as a parameter.
- Multi policy possible.
- Notification possible.