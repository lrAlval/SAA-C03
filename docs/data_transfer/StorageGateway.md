![[Pasted image 20221031110419.png]]
# Storage Gateway

## TLDR
Can be used for a **hybrid cloud** setup, where data is produced on premise and synced to AWS.

![[Pasted image 20230531211257.png]]

## Use cases
- long term migrations
- security
- compliance
- general IT strategy (hybrid cloud)
- tiered storage
- backup and restore
- disaster recovery
- on-premises cache & low-latency file access

## Gateway Types

### [[S3]] File Gateway
- Configured S3 Buckets are accessible **using** the **NFS** or **SMB** Protocol
- Translates save file request to **HTTP**  request to [[S3]]
- Most recently used data is **cached** in file **gateway**, so it doesn't have to be fetched from AWS.
- Can use all tiers except **Glacier.**
- Bucket access using [[IAM]] roles for each file gateway.
- SMB Protocol has integration with Active directory **(AD)** for user authentication.

![[Pasted image 20230531203933.png]]

### FSx File Gateway
- Native access to [[FSxWindowsFileServer]]
- Local **cache** for frequently accessed data
- Windows **native** compatibility (SMB, NTFS, AD)
- Group file shares and home directories

![[Pasted image 20230531204047.png]]

### Volume Gateway
- Block Storage using **iSCSI**  backed by [[S3]]
- backed by [[EBS]] snapshots – can be used to restore on-premises volumes.
- ***Cached volumes***: low latency access to most recent data.
- ***Stored volumes***: entire dataset is **on-premise**, scheduled back-ups to [[S3]]
![[Pasted image 20230531205741.png]]

### Tape Gateway
- uses Virtual Tape library (**VTL**) 
- back data using existing tape-based processes (and **iSCSI interface**)
- for backup **processes** using **physical Tapes**
- can send directly into [[S3]] Glacier

![[Pasted image 20230531210031.png]]

## Hardware appliance
- useful when you don't have any VM for the storage gateway
- Can be **bought** from amazon.com
- Is a hardware **which** will be your gateway (like a firewall)