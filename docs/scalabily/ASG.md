![[Pasted image 20230522185157.png]]
# Auto Scaling Group

## TLDR
A Group of [[EC2]] Instances scaled horizontally, can use an [[ELB]] or work without it if there is no incoming traffic. Can use [[ELB]] or [[EC2]] health checks. Can also be used for [[ECS]] in which case it uses an ECS service as target.

## Features
- scale horizontally
- scale out and in
	- scale out ⇾ add EC2 instances to match increased load
	- scale in ⇾ remove EC2 instances to match decreased load
- Ensure maximum and minimum ECS2 running
- automatically register EC2 with load balancer
- if instance is unhealthy it will be terminated and recreated
- set desired capacity
- must wait for **cooldown period** to expire to scale again
![[Pasted image 20230522194420.png]]
## ASG Launch template
- similar to launch config
- specifies same stuff
- allows for multiple versions of a template
- can mix on demand and spot instances
![[Pasted image 20230522185838.png]]

## Launch configuration (Deprecated)
- defines instance configuration (size etc.)
- AMI
- instance Type
- key pair
- [[SecurityGroup]]
- block device mapping
- can not be modified but must be swapped if already in use

### [[EC2]] Tenancy
- dedicated before other configs
- Take [[VPC]] tenancy config into account

## Instance States

### Standby
- used for maintenance
- won't be terminated if health check fails
- won't receive traffic

## Termination Order
1. Cost (Spot vs. on-demand)
2. the oldest launch configuration
3. the oldest launch template
4. closest to next billing hour

## Scaling Policies

### Simple
- scale by threshold values (CPU > 50%)
- must wait for **scaling** and **health check** to complete to scale again

### Step
- scale by **multiple threshold** values to different configs

### Scheduled
- scale on **predefined** **time** **window**

### Target Tracking
- scale to match the defined metric (e.g., 50% CPU)
- must not wait for cooldown period

### Predictive scaling
- continuously forecast load and schedule scaling ahead
![[Pasted image 20230522190627.png]]
## Scaling Actions

### Rebalancing
Happens when an instance is missing or AZ is changed or Spot shenanigans.
1. Launch new instances
2. Terminate old instances.

### Scaling
Happens for health checks
1. Terminate
2. Launch new

