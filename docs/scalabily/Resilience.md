
| Service / Resource 	| Resilient Boundary 	| Access by default 	| Deployed/Stored 	|
|---	|---	|---	|---	|
| VPC 	| AZ 	| Private 	| Region 	|
| EC2 	| AZ 	| Private 	| AZ 	|
| AMI 	| Region 	| Private 	| EC2 	|
| S3 	| Region 	| Public 	| Region 	|
| Route53 	| Global 	| Private 	| Global 	|
| CloudWatch data 	| Region 	| Public (from AWS or on-premises) 	| Region 	|
| CloudWatch Logs 	| Region 	| Public 	| Region 	|
| CloudWatch Events 	| Region 	| Public 	| Region 	|
