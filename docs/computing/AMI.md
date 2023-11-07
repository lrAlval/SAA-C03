![[Pasted image 20221030221245.png]]
# AMI Amazone Mashine Image

## TLDR
AMIs are preconfigured [[EC2]] Instance templates. Very similar to dockerfiles. But for [[EC2]]. AMIs alow further customisation of your instances, right on startup of an instance. You can create your own custom AMI or choose one aws and 
other users have already build.
- Locked/Unique to single Region.



## Custom AMI
-  Locked to **region** of creation, but can be manually copied to **another** **region**.
- Faster **boot** **time**, because you won't have to install as many or no dependencies.

### AWS Marketplace AMI
- user created AMIs, these might cost money

## How to create your own AMI
- Start [[EC2]]instance
- run scripts/setup and add all data you want the AMI to have
- stop [[EC2]] instance
- build AMI (also creates an [[EBS]] Snapshot, if you delete this snapshot the AMI wont work)
- Launch new instances with your freshly created AMI