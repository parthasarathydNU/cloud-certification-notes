
### Learning 1 SQS Concepts Around Wait time and Retries

**Long Polling** :

> Helps reduce the number of empty responses by allowing the SQS Service to wait until a message is available in the queue before sending a response

***Default Polling*** : This returns a message to the consumer whenever requested, this returns an empty message if the queue is empty
 
***Long Polling :*** The request waits for a specific duration ( 0s  to  max 20s ) before returning. The SQS queue waits during this duration to check for any new message added to the queue, if a message is added within this window, it is immediately returned. This is basically the client willing to wait for a specified time period before requiring a response. 

> This reduces the number of empty responses and decreases the overall cost of using SQS by reducing the number of API calls.

**Wait Time Window**

> This is related to long polling. It defines the duration (in seconds) for which the "*Receive Message action call*" waits for a message to become available in the queue before returning. The max wait time for the window is 20 seconds.

**Re drive Policy**

> A re drive policy is used to handle messages that can't be processed ( failed to process after a certain number of attempts ). *These messages are moved to a dead-letter queue.*  Are these set up by default ? 

**Dead Letter Queue DLQ**: 
A queue that stores messages that fail to process successfully after being retried "maximum receives" number of times.

**Maximum Receives** : 
The number of times a message can be received before it is moved to the DLQ

**Visibility Timeout**

> Period of time during which a message is invisible to other consumers after being retrieved by a consumer. 

Others can't see a message when it is being processed. 

- This ensures that other consumers don't process the same message before the current consumer has completed it's processing.  PREVENTS DUPLICATE PROCESSING - VISIBILITY TIMEOUT ( Be only visible after this timeout )
- If the message is not deleted from the queue within the visibility period timeout, ( assuming the deletion is happening after successful processing ), it is then available to other consumers after the time out to be processed

> Default visibility timeout is 30s , can be increased to up to 12 hours


### Learning 2: AWS Data Sync

*One time and live data migration from on prem to AWS in a secure and fast manner*

> DataSync can be used to migrate files and other objects from on prem to AWS S3 or EFS storage systems in a secure and fast manner. 
> 
> The sync task can be run in multiple cycles where only the delta is synced across the network. 
> 
> Further this can be coupled with a FileGateway that acts as a secure and fast way to read the files that were migrated to the cloud with super low latency through a secure network. 

### Learning 3: Private Subnets and NAT

*NAT Provides internet access to private subnets. NAT is in Public Subnet*

> Subnets are characterized as private or public based on whether they have internet connectivity or not

**Private Subnets** : 
Subnets where there is no route to internet gateway in the route table. They are usually configured to route their traffic through NAT Gateway or NAT instance. 

**Use case:** 

> Private subnets are typically used for the application tier and database tier, where direct internet connection is not required or desirable for security reasons. 

**NAT Gateway**

A managed service provided by AWS that enables instances in a private subnet to connect to the internet or other AWS services, but prevents the internet from initiating a connection to these instances.

- ***NAT Gateways must be places in a public subnet***
- Automatically scaled, highly available, cost is by amount of data processed an duration of time the NAT gateway is used

**NAT Instance**: 

This is basically a manual EC2 instance that is configued to do the task of a a NAT Gateway. It is more cumbersome to maintain and manage as compared to the Gateway. 

However a NAT instnace can act as a bastion host, can support port forwarding and also can be associated with security groups.

**Instances placement**:

> - Application instances are placed in a private subnet that do not allow access from internet as they do not have an internet gateway. 
> - Applications talk to internet and other AWS services through the NAT Gateway / NAT instance that is placed in a public subnet
> - Requests to the internet from the Private Subnet are directed to the NAT gateway, which in turns directs traffic to the internet gateway


### Learning 4 : PREFER S3 over EBS for file storage and higher availability and lower operational overhead

> EBS volumes are tied to the lifecycle of the EC2 instance and the AZ in which the instances are present. This increases the operational overhead when it comes to disaster recovery and migration. 

For applications where shared storage is required, it is wiser to go with EFS, S3 or RDS services that provide high availability, scale with minimal operation overhead and data syncing capabilities. 

EBS is attached to a single EC2 instance within a Single AZ. To share data across EBS instances, additional steps need to be implemented. 

#### Learning 5: You can have one Elastic IP (EIP) address associated with a running instance at no charge.

> More than one elastic IP per instance is charged. Elastic IP that are unassigned are charged. 

This is AWS's way to ensure Public IP addresses are not lying around unused.

### Learning 5: Per the AWS Acceptable Use Policy, penetration testing of EC2 instances May be performed by the customer against their own instances with prior authorization from AWS


### Learning 6: EBS Volume Types

1. Standard - Magnetic Storage:
   Original EBS Storage type. Lowest cost option. Suitable for low throughput infrequent access requirements. Cold Workloads where cost is a primary concern. 
   Max 40 - 200 IOPS, Low Cost
   Throughput: 40 - 90 MiB / s
   
2. General Purpose SSD ( gp2 and gp3 )
   Balance of price and performance suitable for a wide variety of workloads
   **Boot volumes** - Small to medium size databases - dev and test environments
   Max IOPS 16,000, Cost effective for most use cases
   Throughput: 250MiB/s
   
3. gp 3
   Consistent performance and ability to independently scale IOPS and throughput
   Boot volumes, medium size databases, general purpose workloads that require better performance than gp2
   Baseline of 3000 IOPS with ability to scale upto 16,000 IOPS
   Throughtput can scale upto 1000MiB / s
   
4. Provissioned IOPS SSD
   
   io1 : 
   Upto 64,000 IOPS per volume (max using Nitro System )
   Max throughput 1000 MiB / s
   
   io2: 
   Higher durability as compared to io1
   Upto 64,000 IOPS per volume
   99.999% durability as compared to io1 (99.8% - 99.9%)

- **Throughput Optimized HDD (st1)**: Cost-effective for throughput-intensive workloads.
  
- **Cold HDD (sc1)**: Lowest cost for infrequently accessed data.

### Learning 7 : Storage Gateways

*File gateway - Posix Compliant | NAT* 
*Tape Gateway - Long Term storage | Glacier*

[A Quick Report of Gateway Stored Volume v.s. Gateway Cached Volume](https://gkzz.medium.com/a-quick-report-of-gateway-stored-volume-v-s-gateway-cached-volume-3d483c9b2dd7)

Storage gateway is a hybrid cloud storage service that gives you on-prem access to virtually unlimited cloud storage

**Features :**
- Optimized data transfer functions including caching that delivers low latency for frequently accessed data
- **Without modifying client's local infrastructures**
- Compatible with NFS, SMB, iSCSI, and iSCSI-VTL

We get access to leverage both on-prem capacity and latency forwarded data without expanding local environment's capacity.

**Storage Gateway Family**

 > - Volume Gateway : *Provides cloud-backed storage volumes*
 > - File Gateway : *Supports file interface into S3* - Suitable for file systems that follow POSIX Standards
 > - Tape Gateway : *Archive backup data in Amazon Glacier*

 
#### Where do have the data stored when using Storage Gateway

Storage Gateway allows us with two options to store data. One is locally, and the second is on AWS.

![[Screenshot 2024-06-10 at 12.21.56 AM.png]]

**Using On Prem Storage**

Data is stored primarily on-prem. 
- Asynchronously back up data to S3 as EBS snapshots

Useful to help recovering from disasters. ![[Screenshot 2024-06-10 at 12.24.19 AM.png]]

**Cached Mode**

Data is stored primarily on Amazon S3
- Frequently accessed data is stored locally

This is useful if there is a need to minimize scaling on on-prem storage infra. ![[Screenshot 2024-06-10 at 12.26.03 AM.png]]

Here infrequently accessed data is cached and is available at a lower latency from S3. 

- Gateway Stored Volume   -> Stored **by locally** as primary data storage  
- Gateway Cached Volume  -> Stored **by Amazon S3** as primary data storage

### Learning 8 :  Elastic Disaster Recovery

Elastic Disaster Recovery is a service designed to help you recover applications in AWS that are running physical or Virtual Infra in your datacenter or on other cloud environments. RDS enables fast, reliable recovery of apps and data to AWS with minimal downtime.

**Features**

Continuous Data Replication
- Asynchronous, realtime
- *Replication occurs to a staging area* in AWS region of choice minimizing the impact on primary operations

Automated Failover and Fail back
- FailOver: In event of a disaster we can quickly launch recovery instances in AWS using the most recent replicated data. This minimizes recovery time and data loss
- Fail back: Once the primary environment is restored, AWS DRS supports the reverse process, allowing us to replicate data back to original source 

Simple Setup and Management: 
- Straightforward setup process via AWS management console 
- Automated testing capabilities allowing us to test RD plans without impacting prod environment

### Learning 9: NAT Gateways / NAT Instances HAVE TO be placed in the PUBLIC SUBNET

### Learning 10: RDS Multi AZ is for high availability, the secondary AZ is only a standby instance and not meant to be used as READ Replica. CREATE A READ REPLICA IF YOU WANT TO SCALE READS

### Learning 11: Differences between Aurora and RDS in terms of Read Replicas

**RDS** : 

> - We can create read replicas to offload read traffic from primary DB instance. 
> - Replicas can be in same or different region and replicate data asynchronously
> - Read replicas of RDS use standard instances and do not inherently offer high throughput and low latency read capabilities of Aurora
> - There might be a slight delay between primary instance and read replica as it follows eventual consistency model - Might lead to issues if not handled 


**Aurora :**

> - Replicas are tightly coupled into the Aurora Cluster and are *designed to share the same underlying storage,* which is automatically replicated across AZs
> - Faster read performance and lower latency compared to RDS, because they have a shared storage architecture and supports up to 15 read replicas
> - This design allows for instant replication and lower read latency
> - Configure one reader end point to distribute traffic across multiple read replicas
> - Better consistency with it's replication mechanism, replication lag is minimal providing almost real time consistency across the cluster

### Learning 12: Select the "no-reboot" option if you want to create an AMI from a running instance. 

> - If not EC2 shuts down the instance takes a snapshot of attached volumes, creates and registers the AMI and then reboots the instance
> - Note that if we chose no reboot, AWS can't guarantee that the file system integrity of the created image as the snapshot is taken from a running instance

