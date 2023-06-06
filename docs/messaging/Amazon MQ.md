> Managed message broker for open sources queues.

## Features
- Multi-AZ
- Supported protocols:
	- MQTT
	- AMQP
	- STOMP
	- Openwire
	- WSS
	- Websockets
- Need [[EFS]] for failover.

![[Pasted image 20230604164958.png]]

# Message Queue

- Rabbit MQ or Active MQ 
- use for migration if you don't want to migrate app
- multi az availabvle, needs efs for failover
- topic and queue feature (emulate **sqs** and sns)