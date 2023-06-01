![[Pasted image 20221031111028.png]]
# Transfer Family

## TLDR
> Fully-managed service for file transfers into and out of [[S3]] or [[EFS]] using the **FTP** **protocol**.

![[Pasted image 20230531212429.png]]

## Features 
- managed infrastructure
- price per provisioned endpoint per hour + transfers in GB's
- store and manage credentials withing the service .
- Managed infrastructure
- Scalable
- Reliable
- Highly Available (multi-AZ)
- integrate with other auth systems 
	- [[Cognito]], 
	- Lightweight Directory Access Protocol (LDAP)
	- [[AWSAD]]
	- Microsoft Active Directory 
	- Okta
	
## Pricing Model
- pay per provisioned endpoint per hour + data transfers in GB

## Supported Protocols
- AWS Transfer for **FTP** (File Transfer Protocol)
	- unencrypted.
- AWS Transfer for **FTPS** (File Transfer Protocol over **SSL**)
	- encrypted in-flight
- AWS Transfer for **SFTP** (Secure File Transfer Protocol)
	- encrypted in-flight.


## Use Cases
- **ERP**
- **Public Data**
- **CRM**

## Targets
- [[S3]]
- [[EFS]]