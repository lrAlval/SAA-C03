![[Pasted image 20221031093528.png]]
# [[IAM]] Identity Center
>Similar to [[Cognito]] but for access and **auth** to AWS **itself**, rather than Applications running in AWS.

![[Pasted image 20230607194017.png]]

## TL;DR
- formerly known as AWS Single sign-on.
- One Login SSO for all your AWS Accounts.
- **SSO** for business cloud application.
- Support SAML2.0 enabled applications.
- Can be used to grant access to [[EC2]] Windows Instances (remote working PCs).

## Features

### Multi-account Permissions
- Managed across AWS accounts in your AWS org.
- Permissions Sets:
	- will auto create an IAM role for users.
	- Collection of one or more IAM Policies assigned to:
		- users
		- groups.
![[Pasted image 20230607194916.png]]
### Application Assignments
- SSO access to many SAML 2.0 apps:
	- Salesforce.
	- Box.
	- Microsoft 365.
### Attribute-Based Access Control (ABAC)
 - Fine-grained permissions based on users attributes stored in IAM Identity Center.
 - Like tags or titles (e.g.).
	 - Cost center
	 - title (junior, senior)
	 - locale.
 - Use case → define permissions once, then modify AWS access by changing the **attributes**.


## Identity Providers
- Built-in identity store in [[IAM]] Identity Center
- 3rd party.
- AD.
- One Login.
- Okta.
