# CloudFront
- CDN
- ***Global Service***
- ***Cache content all around the world***.
- data, videos, application and apis delivery
- 216 Point of presence globally (edge locations)
- **DDoS** protection , integration with Shield &  AWS Web Application Firewall
- global
- regional edge caches
- only **http** & **https** based requests

## Origins

### [[S3]]
- caching
- distributing
- enhanced security with Origin Access Control (**OAC**)
- CloudFront can be used as an **ingress** (to upload files to S3)

### Custom Origin (HTTP) 
-  [[docs/scalabily/ELB#Application Load Balancer (ALB)|ALB]]
	- Load Balancer must be **public** 
- [[EC2]] 
	- EC2 instances must be **public**
	- allow public ip of edge locations
- [[S3]] Website
- Any HTTP backend

## Geo Restriction
- **white**-list countries
- **black**-list countries
- use for **copyright laws** to control access to **content**

## Price Classes
- depends on **data** **transfer**, but is different for each **edge location**
- price goes down if you transfer **more data**
- price goes down if you reduce the number of **edge locations**
![[Pasted image 20230530163058.png]]

![[Pasted image 20230530163242.png]]

![[Pasted image 20230530163341.png]]
### All
- all regions – best performance – highest price

### 200
- most **regions – excludes most exp

### 100
- only cheapest regions 

## Cache Invalidation
- by default content only get refreshed after **TTL** has **expired**
- invalided via **api** and **path**
	- invalidate all files (*\*)
	- special path (/images/*\*)

## Customization at Edge
- serverless
- customize a **CDN** endpoint
- pay per use

### Use cases
- Website security and privacy
- SEO
- intelligent route
- bot mitigation
- real time image transform
- a/b testing
- Dynamic Web Apps at Edge
- User prior
- tracking ad analytics
- user auth 

### CloudFront Edge function
- code attached to CloudFront distributions
- runs closer to users for min latency
- lightweight written in js
- high scale latency senstive cns customisations
- sub ms startuptimes
- managed in cloudfront
- millions of request per second

#### Price
- Free tier available
- 1/5 of [[Lambda]] @Edge

#### Use cases
- cache key normalisation (transform request attributes)
- header manipulation
- url rewrites and rediect
- validate jwt tokens

### [[Lambda]] at Edge
- **nodeJs** or python
- 1ks of request per second
- can change every part of the request (viewer and origin)

#### Price
- no free tier

#### Use cases
- loner exec time
- adjustible cpu memory
- code depends on 3rd party (AWS CLI)
- Network access
- File System Access
- Http Body Access

## Availability
- can setup origin failover
- an origin group may have a primary and a secondary origin