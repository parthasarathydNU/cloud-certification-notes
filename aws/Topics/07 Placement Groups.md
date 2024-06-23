Placement groups help us control the relative positioning of EC2 instances across hardware. 

The different types of placement group options are - Cluster, Spread, Partition. 

**Cluster Placement Group**
- This places all the instances on hardware that are in close proximity to each other in terms of higher per-flow throughput for TCP and IP traffic
- They are placed in the same high bandwidth network
- Usually these instanced are started on hardware that are there on the same rack in an Availability Zone
- While these instances enjoy a high bandwidth network connectivity, they lack security from hardware failure

To prevent from this type of hardware failure, we have next..

**Partition Placement Group**
- Splits the instances into logical groups called Partitions
- Instances of a partition are spun up on a separate rack and they don't share the same rack as instances of any other partition
- Partitions can be created across AZs in a given region and one partition placement group can have a maximum of seven partitions per AZ
- **EC2 instances get access to partition information as metadata** 

**Use case of partition placement group**
- Application that can be partition aware to distribute data
- Big data applications such as HDFS, Casandra, Kafka

**Spread Placement Group**
- Each EC2 instance is on a different hardware
- Since this PG provides access to different hardware, this will be a good choice for applications that might need different types of instance classes and those which will have instances created over time
- A rack spread placement group restricts more than one instance being spun up on the same rack in a given AZ
- In this case, just like a partition, there is a limitation of 7 running instances in each AZ per rack spread placement group


**Use case of Spread Placement Group**
- Small number of critical applications that need to be Isolated from one another

