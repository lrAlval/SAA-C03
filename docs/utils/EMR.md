#  Elastic Map Reduce
- platform for running big data frameworks
- EMR helps to create **Hadoop clusters**.
- Cluster made of hundreds of EC2 instances.
- EMR comes bundled with:
	- Apache spark
	- HBase
	- Presto
	- Flink
- EMR handle all provisioning and **configuration**.
- Auto-scaling and integrated with Spot **instances**.
- Move and transform data between AWS storage.

## Use cases
- data processing
- machine learning
- web indexing
- big data

## Nodes
- **Master Node**: manages the cluster and health-long running.
- ***Core node***: runs task and stores data- long-running.
- ***Task node***: just runs tasks (**spot** instances)

## Purchasing options
- On-demand: reliable, predictable, won't be terminated.
- **Reserved** (min 1 year): costs savings (EMR will automatically use if available)
	- for master nodes
	- for core nodes
- **Spot Instance**: cheaper, can be terminated, less reliable.
	- for task nodes


## Cluster
- Long-running
- transient (temporary) cluster

## Price
- can any type of ec2 pricing (reserved, spot or on demand)
