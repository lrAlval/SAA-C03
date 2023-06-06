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
- code attached to **CloudFront** distributions.
- Used to change viewer **requests** and **responses**
- Runs closer to users for min **latency**.
- Lightweight **written** in JS.
- high scale latency **sensitive** CNS customizations.
- Sub **ms** startup times.
- Managed in CloudFront.
- Millions of request per second.

#### Price
- Free tier available
- 1/5 of [[Lambda]]@Edge

#### Use cases
- cache key normalization (transform request attributes)
	- Transform request attributes to create an optimal cache key:
		- headers
		- cookies
		- query strings
		- URL
- customize CDN content.
- **Header** manipulation.
- URL rewrites and redirect.
- Validate JWT tokens.


### [[Lambda]] at Edge
- **Node.js** or python
- 1ks of request per second
- can change every part of the request (viewer and origin)

![[Pasted image 20230604230739.png]]

#### Price
- no free tier

#### Use cases
- longer exec time (several ms).
- Adjustable CPU memory.
- Code depends on 3rd party libraries(e.g. AWS SDK to access other AWS services).
- Network access to use external services for processing.
- File System Access.
- HTTP Body Access.

## Availability
- can set up origin failover
- an origin group may have a primary and a secondary origin