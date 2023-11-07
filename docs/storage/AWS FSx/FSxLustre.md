# Amazon FSx for Lustre

## TL;DR
- Fully **managed** service
- Designed for **HPC – Linux workloads Clients
- **Designed** for Machine Learning, Big Data, Financial Modelling
- Can be backed up to [[S3]] 
	- (Manual or Automatic 0–35 days retention)
	
## Access
- [[VPN]]
- [[DirectConnect (DX)]]

## Performance
- Scales up to 100s GB/s, millions of **IOPS**, **sub-ms** latencies

## Use case
- high performance file system
- High Performance Computing (**HPC**)
- Designed for Machine Learning
- Big Data
- Financial Modelling
- Video processing
- Electronic design Automation

## Back-up
- Can be backed up to [[S3]] 
	- (Manual or Automatic 0–35 days retention)

## Storage Options
- **SSD**
	- low-latency
	- IOPS intensive workloads
	- small & random file operations
- **HDD**
	- throughput-intensive **workloads**
	- **large** & **sequential** file **operations**

## Seamless integration with S3
- can “read [[S3]]” as a File System (through FSx)
- can write the output of the computations back to [[S3]] (through FSx)

## Additional Info
- Designed for HPC – Linux workloads Clients
- Fully managed service
- high performance file system
- hot data parallel and distributed

## File System Types

### Scratch File System
>Optimized for **Short term processing – optimize costs** no replication. 
- Fast – Designed for **pure** performance
- **Temp** storage
- High **burst** (6x faster, 200 Mbps per TiB)
- Data is not replicated 
	- doesn't persist if file server fails.
	- NO **HA**, NO **REPLICATION.**

### Persistent File System
> Long-term processing – sensitive data**
- Longer term storage
- Data is replicated withing same **AZ** – HA (IN ONE AZ)
- replace failed files within **minutes**
- Self-healing



