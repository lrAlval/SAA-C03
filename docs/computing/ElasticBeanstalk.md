![[Pasted image 20221030232727.png]]
# Elastic Beanstalk

## TLDR
A quick way of hosting an application without having to manage infrastructure. But you can modify your infrastructure post launch. It offers more control than [[AppRunner]]. 

Features
- Beanstalk is free but you pay for the underlying instances (EC2,ASG,ELB,RDS)
- full control over the configuration
- supports docker
- app logs are saved to [[S3]]
- server logs can be enabled and saved to [[s3]] or [[CloudWatch]]

## Components
- App: collection of Elastic beanstalk components (envs, config, versions)
- App Version: an iteration of your app code
- Environment:
	- collection of AWS resources running an app
	- Tiers: web server env tier & worker env tier
	- can create multiple envs (dev, test, prod)

## Deployment Modes
- Single Instance : great for testing or dev
- High Availability with Load balancer: Great for prod

![[Pasted image 20230527122330.png]]