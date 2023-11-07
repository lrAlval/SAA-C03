# Choose a volume

## EBS
- can only be attached to **one instance** (except multi-attach io1/io2)
- **single AZ**
- gp2:io increases if the disk size increases .
- io1: can increase io independently.
- To migrate an EBS volume across **AZ**
	-  take snapshot
	- restore snapshot to another **AZ**
	- EBS backups use io, and you shouldn't run them while your app is handling lot of traffic.
- By default: Root EBS volumes of instances get terminated when the [[EC2]] instance gets terminated. (you can disable that)

## EFS 
- Goal: simplify setting and managing **shared file storage** in cloud env.
- Main purpose is mounting 100 of Linux ec2s across **AZ's** 
- **more expensive** than EBS
- **EFS** share websites files (WordPress)
- can leverage **EFS-IA** for cost savings.
![[Pasted image 20230521231243.png]]
## Instance Store
- I need max iops
- useful when data is not critical & is replaceable
- Good for **buffer**, cache **,** scratch data, temporary content.