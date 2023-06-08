![[Pasted image 20221031085227.png]]
# Directory Service
>A collection of sub services which allows companies to leverage directory authentication within AWS. Supports Microsoft Active Directory.

## Versions

### AWS Managed Active Directory
- Can also be used **on-premise**, 
	- 2 side trust connection is established between AWS AD and **on-premise AD**.
- users shared between on-premise **AD** and AWS managed AD**.**
- out-of-the-box integration with [[IdentityCenter]].
	![[Pasted image 20230607200825.png]]
- **AD** is managed on **AWS side**.
- Can:
	- manage users **locally**.
	- Support **MFA**.
![[Pasted image 20230607200316.png]]

## AD Connector
- Can use on-premise ad **auth** in AWS, by **proxying** to the ad domain controller on premise.
-  out-of-the-box integration with [[IdentityCenter]].
- AD is **managed** on premise.
	- users on-premise **AD**.
- Supports **MFA**.

![[Pasted image 20230607200549.png]]

## Simple AD
- Create a new AD managed in AWS.
- No on-premise AD required, but can be joined.
