
## S3
- Object Storage
### S3 Glacier
- Object archival

## EBS volumes
- network storage for ONE EC2 instance at a time.
- Cheap
- **Single-AZ.**

## Instance Storage
- Physical storage for EC2 instances (high **IOPS**)
- useful for cache stores
- Temp data

## EFS
- Network file system for Linux instances
- POSIX FS
- scalable and **expensive**
- mounted across **Multi-AZ**

## FSx for Windows
- Network file system for **Windows** **servers**

## FSx for Lustre
- HPC Linux FS

## FSx for NetApp ONTAP
- High **OS** compatibility for a network file system
- Compatibly with **NFS**, **SMB**, **iSCSI**.

## FSx for OpenZFS
- Managed **ZFS** file system
- 

## Storage Gateway
- bridge **storage** between on-premises and AWS
- Storage Types:
	- S3 
		- access protocols: 
		- NFS 
		- SMB protocol
		- supports AD for auth.
	- FSx File Gateway 
		- access protocols: 
			- NFS 
			- AD
			- SMB protocol
	- Volume Gateway (cached & stored) 
		- – mount volumes on-premises servers
		- access protocol:
			- iSCSI
	- Tape Gateway 
		-  backs-ups in tape form.
		- access protocol:
			- iSCSI

## Transfer Family
- FTP, FTPS, SFTPS interface on top of:
	- S3
	- Amazon **EFS**

## DataSync
- Schedule data sync from on-premises to AWS.
- data sync from **AWS** to **AWS**

## Snowcone / Snowball / Snowmobile
- move large amount of data to AWS physically.
- migrate large amounts of data **without** **internet**.