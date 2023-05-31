![[Pasted image 20221031092405.png]]
# AWS Control Tower

## TLDR
Control Tower is often used in conjunction with [[AWS Organizations]]
to manage and configure a multi account setup.

![[Pasted image 20230515180648.png]]


## Benefits
- Automate setup of [[AWS Organizations]]
- Automate policy management using guard rails
- Detect policy violations
- Monitor compliance through dashboard
- Streamline account creation in [[AWS Organizations]]

## Elements
- Landing zone - **multi-account** env
	- SSO/Id federation, Centralised Logging & Auditing.
- Guard Rails - **Detect**/**Mandate** rules/standards across all accounts.
- Account Factory - **Automates** and **Standardises** new account creation.
- Dashboard - single page oversight of the entire env.

## Landing Zone
-[[IdentityCenter]] = SSO  multiple-accounts, Id Federation
- Monitoring and Notifications = CloudWatch and SNS
- built with [[AWS Organizations]] , [[AWSConfig]], [[Cloudformation]]
- Security OU = Log Archive & Audit Accounts ([[CloudTrail]] & Config Logs)
- Sandbox OU = Test/less rigid security.
- you can create other OU's and accounts.
//TODO: add aws service catalog page
- End User account provisioning via [[# AWS Service Catalog]]

## Guardrails

### Preventive Guardrail
- uses [[AWS Organizations]] SCP
- e.g. restrict regions across all accounts
- rules - multi account governance
- Mandatory, Strongly Recommended or Elective. (enforced or not enabled)
	- **Preventive** => Stop you doing things  [[AWS Organizations#Serve Control Policies (SCP)|SCP]]
	- **Detective** => compliance checks [[AWSConfig]] Rules.
		-  e.g. identify untagged ressources
	- they are either in **clear** , **in violation** or **not enabled**.

### Account Factory
- automated account provisioning
- **cloud admins** or **end users** (with right set of permissions)
- Guardrails - **automatically** added to all acounts
- accounts can be **closed** or **repurposed**
- account & network **standard configuration**
- can be fully **integrated** with a business **SDLC**.


## Further Integration
- [[SNS]]