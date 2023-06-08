![[Pasted image 20221031085836.png]]
# AWS Organizations

## TLDR
This is a service to manage multiple accounts and big user count at a central place. Also has features regarding pricing and setting standards.

## Features
- Group multiple AWS accounts
- **Global** service
- **Manage** multiple accounts
- There is one main account which is the root, the other accounts  join the [[AWS Organizations]] of the root account as member accounts
- Shared resources possible (See [[VPC]])
- You can leverage the API to quickly create new AWS accounts
- Can use a central [[S3]] account for logs
- **Central audit account**

## Advantages
- Multi account vs. one account multi [[VPC]].
- Use ***tagging*** standards for billing purposes.
- Enable [[CloudTrail]] on all accounts, send logs to central [[S3]] account.
- Send [[CloudWatch]] Logs to central logging account.
- Establish ***Cross Account Roles*** for admin purposes.

## Limitations
- A single account can not be in two **different organizations**.

## Cost Management
- Consolidated **billing** makes monthly fees for some resources, which are used by multiple accounts within the [[AWS Organizations]], only be paid once (E.g. [[AWSShield]]).
- Benefits for aggregated usage of resources and services.
- Share reserved [[EC2]] instances and savings plans between your AWS  accounts.


## Structure
![[Pasted image 20221031091158.png]]

### Serve Control Policies (SCP)
- SCPs are account **permissions** boundaries.
- Must have an explicit allow.
	- does not allow anything by default like **IAM**.
- [[IAM]] Policies for Account Groups (OUs).
	- ![[Pasted image 20230607191003.png]]
- Affect **all users** even to the ***root user***.
- They don't grant any permissions.
	- SCPS are a way of restricting the actions that can be taken in an AWS account so that all IAM users and roles, and even the root user, cannot perform them.
- When an SCP is created
	- it creates a ***FullAWSAccess*** policy, so it doesn't restrict anything.   
- [[IAM]] Policies for Account Groups (OUs)
- Affect all users even the root user
- Don't affect service linked policies (like [[S3]] bucket policy)
- use for **denies** cross account in your org
![[Pasted image 20230510200104.png]]

![[Pasted image 20230607191559.png]]

### (SCP) [Use Cases](https://summitroute.com/blog/2020/03/25/aws_scp_best_practices/#two-person-rule-concept)
- Deny ability to make a **VPC** accessible from the Internet that isn’t already.
- Deny ability to modify an important IAM role.
- Deny ability to disrupt CloudWatch Event collection.
- Deny ability to disrupt [[GuardDuty]].
- Deny ability to leave Organization
- Region enforcement.
- Deny ability to create **IAM** access keys.
- Require the use of IMDSv2.
- Deny root user access.
- Allow only approved services.