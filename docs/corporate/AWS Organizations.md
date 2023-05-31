![[Pasted image 20221031085836.png]]
# AWS Organisations

## TLDR
This is a service to manage multiple accounts and big user count at a central place. Also has features regarding pricing and setting standards.

## Features
- Group multiple AWS accounts
- Global service
- Manage multiple accounts
- There is one main account which is the root, the other accounts  join the [[AWS Organizations]] of the root account as member accounts
- Shared ressources possbile (See [[VPC]])
- You can leverage the API to quickly create new AWS accounts
- Can use a central [[S3]] account for logs
- Central audit account

## Limitations
- A single account can not be in two different organisations

## Cost Management
- Consolidated billing makes monthly fees for some ressources, which are used by multiple accounts within the [[AWS Organizations]], only be payed once (E.g. [[AWSShield]])
- Benefits for aggregated usage of ressources and services
- Share reserved [[EC2]] instances and savings plans between your AWS  accounts


## Structure
![[Pasted image 20221031091158.png]]

### Serve Control Policies (SCP)
- SCPs are account permissions boundaries
- They don't grant any permissions.
	- SCPS are a way of restricting the actions that can be taken in an AWS account so that all IAM users and roles, and even the root user cannot perform them.
- when an SCP is created
	- it creates a FullAWSAccess policy , so it doesn't restrict anything.   
- [[IAM]] Policies for Account Groups (OUs)
- Affect all users even the root user
- Dont affect service linked policies (like [[S3]] bucket policy)
- use for denies cross account in your org
![[Pasted image 20230510200104.png]]

### (SCP) [Use Cases](https://summitroute.com/blog/2020/03/25/aws_scp_best_practices/#two-person-rule-concept)
- Deny ability to make a VPC accessible from the Internet that isn’t already
- Deny ability to modify an important IAM role
- Deny ability to disrupt CloudWatch Event collection
- Deny ability to disrupt GuardDuty
- Deny ability to leave Organization
- Region enforcement
- Deny ability to create IAM access keys
- Require the use of IMDSv2
- Deny root user access
- Allow only approved services