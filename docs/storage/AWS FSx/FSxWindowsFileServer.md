# Amazon FsX for Windows File Server

## TL;DR
- **fully** managed windows FS **share drive**
- **highly** reliable
- **SMB** protocol & Windows **NTFS**
- Scale up to **10s** of GB/s, millions of **IOPS**, 100s **PB** of data.
- **AD** Integration, access control lists (**ACLs**), user quotas
- can be mounted on Linux **EC2 instances**.
- Supports Microsoft distributed FS (**DFS**) 
- Namespaces (group files across multiple **FS**)
- Can be configured to be **Multi-AZ** (**HA**)
- Data is backed-up daily to **S3**.
- Can be accessed from your **on-premises** infrastructure:
	- [[VPN]], 
	- [[DirectConnect]]


## Longer Version
- Fully managed native Windows file **servers/shares**
- designed for **integration** with **Windows environments.**
    - **Native** Windows file system, **not emulated server**
- Integrates with Directory Service or Self-Managed **AD**
- Can be used in **Single** or **Multi-AZ** within a [[VPC]].
    - This controls the **network** interfaces that are **available**.
    - **Single mode** use replication in the **AZ** to ensure **resiliency**.
- Can perform **full range** of **different backups**
    - **Client side** and **AWS side**
    - Can perform **automatic** and **on-demand** **backups**.
- File systems can be access using:
	- [[VPC]], 
	- Peering
	- [[VPN]], 
	- [[DirectConnect]]
	- Native windows FS or Directory Services.

#### Words to look for

- **VSS**: User Driven Restores
- Native File System (**NFS**) accessible over SMB
- Windows permissions model
- Product supports Distribute File Systems (DFS), scale out file share.
- Managed service, no file server admin
- Integrates with DS and your own directory.