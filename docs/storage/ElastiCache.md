![[Pasted image 20221101164642.png]]
# Elasticache

## TLDR
Volatile Caching Layer with high performance.

## Features
- in memory data store
- managed [[Redis]] or [[Memcached]].
- Boost performance of databases
- use cases caching, session stores, gaming, geospatial services, real time analytics and queuing
- for relational databases caching layer
- helps make app stateless
- AWS managed (OS, patching, monitoring, failure recover, backups)
- requires app changes.

## Use Cases
- read **heavy** **HPC** tasks
- **compute** heavy HPC **tasks**
- session stores
- high **performance DB caching**
	- **Gaming Leaderboards**
	- 

## Redis
- see [[Redis]]

## Memcached
- open source memory store
- multithreaded
- no replication
- no snapshots
- no transactions
- no pub/sub
- no geospatial support
- no Lua scripting
- no high availability
- Sharding
- non-persistent
- no backups
- support **Simple Authentication and Security Layer** (SASL) based auth

## Security
- no [[IAM]] Auth
- IAM policies used only for AWS API-level security
- can us  SSL encryption for in flight

## Loading patterns
- **lazy** (all read data is **cached**)
	- data **can become stale**.
- Write **through** (adds or updates to the db are mirrored in the cache) 
	- **no stale data**.
- **Session** store (expire data with **time to live**)
	- **no stale data**.