![[Pasted image 20221031103135.png]]
# AWS Data Sync

## TLDR
>**Data Sync** is used for a secure one time transfer of data via the **internet** from a **source** into AWS.

## Features
- accelerates copying large amounts of data between a source and AWS
- large scale migrations amounts of data processing transfers.
- File permissions and metadata are preserved.
	- Transfers metadata and timestamps.
- Can use **bandwidth limiters** to avoid **customer** impact
- Supports incremental and scheduled **transfer** options
- **Compression** and **encryption** in transit is also supported
- Has built in data validation and automatic recovery from **transit** errors.
- Sync data can be schedule on hourly, daily or weekly basis.
- Pay as you use product.


## Performance
- Designed to work at huge scales. 
- One **agent** can handle 10 **Gbps**, can setup a **bandwidth** limit. 
- A job can handle 50 **million** files.
- Each agent is about 100 TB per day.

## Security
- File Permissions and metadata are preserved
	- Support **NFS** POSIX & SMB Permissions.

## Use Cases
- one time transfers of data which no longer need to be in other location synced
- Large scale migrations.
- Large amounts of data processing transfers.

## Sources
- On-premise
- Edge
- Other clouds to **AWS** using any of these protocols:
	- NFS
	- SMB
	- **HDFS**
	- S3 API
	- **needs agent**
- **AWS** to AWS (different storage services)
	- no agent needed

## Targets
- [[S3]]
- [[EFS]]
- [[FSxLustre]]
- [[FsxNetApp ONTAP]]
- [[Amazon FSx Open ZFS]]
- [[FSxWindowsFileServer]]
- On-premises


## Examples

## On-premise sync to AWS 
> Using NFS/SMB

![[Pasted image 20230531231204.png]]




## Data Sync Agent
- Runs as a **vm** on premises
- used when connecting to:
	- NFS Server
	- SMB Server

## S3 Outpost
- Runs on EC2 on the outpost

## Snowcone
- Agent comes pre-installed on **a physical** device
- useful when there is no internet access available.


## Route
- On premise File System → On premise Data Sync Agent → AWS [[DirectConnect]] or Internet → AWS [[DataSync]] service → Cloud storage 


#### Data Sync Components

### Task
- job within data sync
- defines what is being synced how quickly
- defines two locations involved in the job
### Agent
- software to read and write to on-premise such as NFS or SMB
- used to pull data off that store and move into AWS or vice versa
### Location
- every task has two locations `FROM` and `TO`
- example locations:
	- network file systems (NFS), common in Linux or Unix
	- server message block (SMB), common in Windows environments
	- AWS storage services (EFS, FSx, and S3)