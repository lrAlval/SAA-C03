![[Pasted image 20221101130307.png]]
# Eastic File System

## TLDR 
High performance network file system which is pay per gb use and can attach to multiple services in multiple AZs.

## Features
- multi-AZ
- high avalilable, scalable and **expensive** ( 3x gp2)
- pay per use
- uses [[SecurityGroup]]
- private service, via mount targets inside a [[docs/networks/VPC]]
- can be accessed from on-premises - [[VPN]] or DX
- General Purpose and Max I/O performance Modes

## Uses cases
- Content Management, web serving, data sharing, wordpress
- **NFSv4.1** protocol
- Only compatible with Linux based [[AMI]]
- encyption at rest with [[KMS]]
- **posix** file system

## Performance
- 1000s of clients 10GBs throughput
- Can handle petabyte scale data

### Performances Modes
- set at creation time

#### General purpose
- web server, cms , file serving
- latency sensitive
- default for 99.9% of uses

#### Max IO
- **higher** **latency** and throughput
- **paralell**
- big data, media processing

### Throughput modes
- Bursting
- Provisioned

#### bursting
- 1 tb = 50mbs + burst of up to 100mbs
- like gp2 volumes inside a [[EBS]]
- throughput scale with the size of the file system
- generally default for wide variaty of cases

#### provisioned
- set **throughput** regardless of size
- more like io1 from [[EBS]]
- use when data created is small but performance needs to be high

## Storage classes

### Storage Tiers
- livecycle managemet for cost savings
- uses **livecycle** policies

#### Standard 
- frequently access files
- default for almost all use cases
- data redundancy across multiples **azs**

#### Infrequent access
- cost to retrieve files but lower storage costs
- designed for infrequent store

## Availablity

### Standard 
- **multi AZ**

### One Zone
- one AZ
- good for testing env
- compatible with infrequent acess ( for up to 90% in savings)
- backup enabled by default

