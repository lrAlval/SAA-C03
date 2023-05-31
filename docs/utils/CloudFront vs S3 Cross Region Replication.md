### CloudFront:
- Great for ***static content*** that must be available ***everywhere.***
- Global Edge network.
- Files are cached for a **TTL** (maybe a day)



### [[S3]] Cross Region Replication
- Great for ***dynamic content*** that must be available at ***low-latency*** in a ***few regions***.
- Replicate **buckets** into other **regions**
- ***Read only.***
- Must be setup for each Region
- Files are updated in ***near real-time***.