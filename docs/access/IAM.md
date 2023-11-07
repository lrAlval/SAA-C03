![[Pasted image 20221030213328.png]]
# Identity and Access Management

## TLDR
- AWS IAM is a global service. 
- It's used in nearly all other services to control permissions and interaction boundaries in regard to resources and services in your account. 
- It's also required to manage users in your AWS Account or [[AWS Organizations]]. Permissions come in the form of groups, role, and policies.

![[Pasted image 20230607185949.png]]

### Limitations 
- **5k** **IAM** Users per account
	- alternatives IAM Roles & Identity federation.
- **IAM** User can be a member of up to **10** **groups**.
- **300** **Group** Limit per account.
	- This can be **fixed** with a **support ticket**.
- No nesting between **groups**.
- No Limit of users in a **group**.
- No default “***all-users-group***” that holds all users in **account**.


### Defaults
- two policies assigned to IAM Role 
	- Permissions Policy.
	- Trust Policy.

### Best Practices
- Don't use your **root account** for anything but **account setup**.
- One **physical users** should also be one AWS user.
- Use **IAM groups** to manage permissions for multiple users.
- Use a **password policy** to prevent weak passwords.
- Use and enforce **MFA**.
- Use **roles** for services.
- Use access keys for accessing services.
- ***Audit*** permissions with ***IAM Credential Report***.
- Never share keys or user.
- Use the ***least privilege*** principle.

## Users
- Real persons.
- Can have multiple or no groups.

## Groups
- Collection of users.
- One group can have multiple users.

## Roles
- Intended to be used by AWS Services.
- if have more than 5000 principals, it could be a candidate for an IAM Role.
- Can be used to access cross account resources.

## IAM Permission Boundaries
- supported for users and roles
- set max permissions an **IAM** entity can get.

### Use case
- allow **devs** to self-assing polices, while making sure they can't escalate their privileges.
- Useful to restrict one specific user.

![[Pasted image 20230607193103.png]]
![[Pasted image 20230607193213.png]]
## Roles use cases
- Cross Account Access
- Adding AWS into existing Corp environment
- Web Identity Federation
	- uses IAM roles to allow broader access. These allow you to use an existing web identity such as google, Facebook, or Twitter to grant access to the app.

## Permission Boundary
- maximum permission employees can grant to other entities.
- Uses managed policies.
- Is attached to principal (which is the AWS Account).
- Can only be set on users and roles.

## Policies
- Handles permissions.
- Attached to group, user, or role as a **JSON** document.
- Should use the least privilege principle.
- If a user has multiple groups, his permissions will be the composition of all policies of all groups.
- Deny always overwrites any allow.

```json
{
    "Version":"date", //required
    "Id":"string", //optional
    "Statement": [ // atleast 1 required
        {
            "Sid": "", // statement id optional
            "Effect" : "", // Allow | Deny
            "Principal" : "", // which account/user/role this should be applied to (only if used to attach to a ressource)
            "Action": [ // list of actions to deny or allow 
                "s3:putObject"
            ],
            "Ressource":["mybucket/*"], // list of ressource for which the actions are applied to
            "Condition": []//list of conditions for when this policy is applied, optional
        }
    ]
}
```

### IAM Policy Conditions
```json
"Condition": 
{ 
	"NumericLessThanEquals": {"aws:MultiFactorAuthAge": "3600"} 
}
```
- Restrict by **client IP**.
- restrict by **target region**.
	- "aws:RequestedRegion"
- Restrict by **tag** (user and resource).
- Force **MFA**.
- Restrict by ***PrincipalOrgId***
	- restrict any resource access to accounts that are member of an organization. 
- Account org.

### Trust Policy
- Defines/Limits which resource an assume the IAM role.

## Password Policy

### Password limitations
- minimum length.
- Include uppercase.
- Include lowercase.
- Include non-alphanumeric.
- Numbers.
- No reuse.
### Other Features
- deny or allow password change by user himself.
- Expiration date.

## MFA

### Virtual MFA Device
- Google Auth.
- Authy.

### U2F (Universal 2nd Factor Security Key)
- 3rd Party device.
- Support multiple users for one device.

### Hardware Key FOB MFA Device
- 3rd party.

### Hardware Key FOB MFA Device for US Gov Cloud
- 3rd party.

## IAM Security Tools

### IAM Credentials Report
- Report of all  Accounts Users and credential status:
	- Password.
	- Access keys.
	- MFA.

### IAM Access Advisor
- target a single user or resource and get the info of all service permissions and when that service was lastly accessed.
- Can be used to revise policies and roles.

## Roles vs. Resource Based Policies
- when you assume a role, you give up all previous permissions.
- Resource based if an ***IAM*** entity needs to do multiple things on different accounts.

### [[EventBride]]
- when [[EventBride]] runs any task it needs access for the target service.
- Some service support ***IAM*** some use **resource** based policies.
	- Resource-based policy:
		- Lambda.
		- SNS.
		- SQS.
		- CloudWatch Logs.
		- API Gateway.
	- IAM Role:
		- Kinesis Stream.
		- System Manager Run Command.
		- ECS Task.
		
![[Pasted image 20230607192837.png]]

### Cross Account
- attach **policy** to a resource ([[S3]]).
- Use a role as a **proxy** (give role access).