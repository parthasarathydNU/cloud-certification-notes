
Managed network file system - that can be mounted to different EC2 instances in different AZs
Highly available, scalable and expensive! ( 3x cost of gp2 volumes ) and pay per use model.

![[Pasted image 20240320104123.png]]

Use cases of EFS
- Content Management
- Web serving
- Data Sharing
- Wordpress

To access EFS we need to set up Security Groups

**Only compatible with Linux Based AMIs (not windows)**

Can set up encryption at rest using KMS and uses POSIX file system ( hierarchical namespace convention ) as the standard API - so can be used as the primary file system and scalable automatically

### Performance and Storage Classes

EFS Scale
- 1000s of concurrent NFS clients, **10 GB+/s throughput** !
- Grow to a **Petabyte**-scale network file system automatically

**Performance modes**
- General Purpose (Default) - Latency sensitive use cases ( Web applications, CMS, etc.. )
- Max I/O - High latency but better throughput and parallel (Media processing and Big Data Applications)

**Throughput modes**
- Bursting - 50 MiB/s + **burst** up to 100MiB/s
- Provisioned - Fixed regardless of storage size , Eg: Maintain throughput to 1 GiB/s until 1 TB of storage
- Elastic - Automatically scales throughput up or down based on workloads
	- Eg: up to 3GiB/s for reads and 1 GiB/s for writes
	- For unpredictable workloads


### Storage Tiers

Feature to move files for storage after a few days ( Lifecycle management feature )
1. Standard Tier - for frequently accessed files
2. Infrequent Access ( EFS-IA ) : cost to retrieve files higher but lower cost to store
	1. Need to attach lifecycle policy along with EFS to enable this

![[Pasted image 20240320104251.png]]

### Availability and Durability

- Standard - Multi-AZ, great for prod
- One Zone: One AZ, great for dev, backup enabled by default, compatible with IA ( EFS One Zone IA ) **90% in cost saving - aggressive discount**


## Summary: 

While setting up EFS (File System) we have the following options that we must consider before setting it up:

1. Performance mode (2) - Standard / High throughput
2. Throughput mode (3) - Bursting / Flexible / Provisioned
3. Storage tier ( 2 ) - Standard , IA, 
4. Availability and durability (2) - Multi Zone / One Zone  ( cost savings )

### Notes
1. When setting up EFS, there are a couple of options under lifecycle management - these policies are enforced at a file level. Interesting
	![[Pasted image 20240320105606.png]]

	![[Pasted image 20240320105753.png]]
	For the exam we only need to remember Bursting - Elastic and Provisioned.
	


Further if we look into the network settings we notice that, the EFS has multiple Mount Targets available across different AZS and they are all attached to the same security groups.

The subnets are the ones assigned by default and each mount target has a private IP address. Need to check if we can access the same file in all the mount targets .. or are they like different folders. 
	![[Pasted image 20240320110235.png]]