![[Pasted image 20221030231124.png]]
# Elastic Container Service
>ECS is AWS Docker Service. You can launch and modify containers as tasks in multiple ways depending on your application and scale.

## Features
- support  NLB, ALB
- support block storage – EFS
	- use case → persistent multi-AZ shared storage for your containers.
	- [[S3]] can't be mounted in EC task.
- 

# Launch Types

## [[EC2]] Based
- Need to have a running [[EC2]] as the host for your containers
- you must provision & **maintain** the **infrastructure**.
- You are billed for depending on the [[EC2]]
- The [[EC2]] Instance must be running  the ECS agent

![[Pasted image 20230604175843.png]]
## Fargate Based / ECS Cluster
- No need to provision-**Serverless**
- Need tasks **definitions**
- Billed for **CPU** and **memory** used
- by default **20gb** of free block storage

## Roles

### Instance Profile
- used by the **ECS Agent**
- Only used for host [[EC2]]
- Used to create and run image on [[EC2]] 

### Task Role
- Defines Permissions for the **code** running in the **container** (access to other services)
- each task can have a specific role 
![[Pasted image 20230604175349.png]]
## ECS Fargate Autoscaling
- Scale on **CPU**, **Mem** or [[docs/scalabily/ELB#Application Load Balancer (ALB)|ALB]] traffic per target
	- ALB Request count per target - metric coming from ALB
- Scaling Fargate is easier
- Combine ECS cluster capacity prover paired with Auto Scaling group

### Modes
- **Target tracking**
	- Scale based on **target** value for specific **[[CloudWatch]] metric**
- **Step calling**
	- Scale based on **specific** **[[CloudWatch]] Alarm**
- **Scheduled scaling**
	- Scale based on specific **date/time** (predictable changes)

## EC2 Autoscaling

- Horizontal scaling.
	- Add more [[EC2]] instances.
- **Auto Scaling Group scaling.**
	- Scale  your ASG based on CPU utilization.
	- Add [[EC2]] instances over time.
- **EC2 Cluster **capacity provider**.**
	- Used to auto provision and scale the infra for your ECS tasks.
	- Capacity provider paired with an auto-scaling group
	- add [[EC2]] instances when you are missing capacity (CPU, RAM)

![[Pasted image 20230604192104.png]]

## Advanced Use Cases
- Use [[EventBride]] or [[docs/messaging/SQS]] to launch container, process tasks and shut down container **afterward**
e.g:

![[Pasted image 20230604192257.png]]

![[Pasted image 20230604192330.png]]

![[Pasted image 20230604192400.png]]

![[Pasted image 20230604192433.png]]