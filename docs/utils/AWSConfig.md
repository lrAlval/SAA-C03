# TL;DR
- Detailed view of the config of **AWS** **resources**.
- Used for **audit** and **compliance**.
- Relations over time.
- **Changes** over time.
- Can stream **changes** and **rules** notifications to SNS.
- Can have configured remediation on non-**compliance rules**.

## Features
- Multi-account
- Multi-region
- can save config-records to s3 bucket of choice.
- Receive a notification whenever a resource is **created**, **modified**, or **deleted**.

## Rules
- **predefined** and **customizable**.
- If a resource violates a rule, Config flags the resource and the rule as noncompliant, and notifies you through Amazon SNS.
- Evaluates your resources either **in response to configuration changes** or **periodically**.
- Did I import a bad cert?

### Conformance Packs
- a collection of AWS Config rules and remediation actions that can be easily deployed as a single entity in an account and a Region or across an organization in AWS Organizations.

### **Config rule**
- Represents your desired configuration settings for specific AWS resources or for an entire AWS account.
- Provides customizable, predefined rules. 
	- If a resource violates a rule, Config flags the resource and the rule as noncompliant, and notifies you through [[SNS]].
- Evaluates your resources either **in response to configuration changes** or **periodically**.

### **Conformance Packs**
- A collection of rules and ***remediation*** actions.
- Created using a YAML template with a list of managed or custom rules and remediation actions.
- Process checks enable you to list compliance of requirements and actions at a single location.

- Config deletes data older than your specified retention period. The default period is 7 years.
- **Multi-Account Multi-Region Data Aggregation**
    - An aggregator collects configuration and compliance data from the following:
        - Multiple accounts and multiple regions.
        - Single account and multiple regions.
        - An organization in AWS Organizations and all the accounts in that organization.

![AWS Training AWS Config 2](https://td-mainsite-cdn.tutorialsdojo.com/wp-content/uploads/2018/12/AWS-Training-AWS-Config-2.jpg)

## **AWS Config Monitoring**

- Use Amazon SNS to send you notifications every time a supported AWS resource is created, updated, or otherwise modified as a result of user API activity.
- Use Amazon CloudWatch Events to detect and react to changes in the status of AWS Config events.
- Use AWS CloudTrail to capture API calls to Config.

## **AWS Config Security**

- Use IAM to create individual users for anyone who needs access to Config and grant different permissions to each IAM user.

## **AWS Config Compliances**

- ISO
- PCI DSS
- HIPAA
- FedRAMP

## **AWS Config Pricing**

- You are charged based on the number of configuration items recorded and on the number of AWS Config rules evaluations recorded, instead of the number of active rules in your account per region.
- You are charged only once for recording the configuration item.
- You are charged per conformance pack evaluation per Region.

