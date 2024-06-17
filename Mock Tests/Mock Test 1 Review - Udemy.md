### Ways of the exam:
- Most of the options will seem relevant
- Read the question completely and pick on key words with respect to 
  1. Cost
  2. Speed of implementation
  3. Efficiency
  4. Reliability / Availability
- Read each question completely sometimes when questions are lengthy it is easier to miss out on details but take a deep breath and take it slow

### Wrong Answers

#### Situation
The engineering team at an e-commerce company has been tasked with migrating to a serverless architecture. The team wants to focus on the key points of consideration when using AWS Lambda as a backbone for this architecture.

##### Options
1. Since AWS Lambda functions can scale extremely quickly, it's a good idea to deploy a Amazon CloudWatch Alarm that notifies your team when function metrics such as `ConcurrentExecutions` or `Invocations exceeds the expected threshold` {Correctly Selected}
   
2. Serverless architecture and containers complement each other but you cannot package and deploy AWS Lambda functions as container images {Not correct and did not select}
   
3. AWS Lambda allocates compute power in proportion to the memory you allocate to your function. AWS, thus recommends to over provision your function time out settings for the proper performance of AWS Lambda functions {Incorrect - selected}
   
4. If you intend to reuse code in more than one AWS Lambda function, you should consider creating an AWS Lambda Layer for the reusable code { correct - missed selecting }
   
5.  The bigger your deployment package, the slower your AWS Lambda function will cold-start. Hence, AWS suggests packaging dependencies as a separate package from the actual AWS Lambda package {Incorrect selected }
   
6. By default, AWS Lambda functions always operate from an AWS-owned VPC and hence have access to any public internet address or public AWS APIs. Once an AWS Lambda function is VPC-enabled, it will need a route through a Network Address Translation gateway (NAT gateway) in a public subnet to access public resources {correct - did not select}


------------------------------------------------------------------------

### New points learnt

#### **Learning 1** : AWS Lambda functions always operate from an AWS-owned VPC

> By default, AWS Lambda functions always operate from an AWS-owned VPC and hence have access to any public internet address or public AWS APIs. 
> 
> Once an AWS Lambda function is **VPC-enabled**, it will need a route through a **Network Address Translation gateway (NAT gateway)** in a public subnet **to access public resources**

![[Screenshot 2024-05-23 at 1.07.12 AM.png]]

#### **Learning 2**: AWS Lambda Layer

*reuse code - more than one lambda function - consider lambda layer - max size 250 mb*

> If you intend to reuse code in more than one AWS Lambda function, you should consider creating an ***AWS Lambda Layer*** for the reusable code
> 
> We can configure AWS Lambda Function to pull in additional code and content in form of layers. A layer is a ZIP archive that contains binaries, a custom runtime or other dependencies. To keep deployment packages small, we can use layers - a function can use upto 5 layers at a time. Total unzipped size of a function and all the layers cant exceed 250 megabytes. Layers support resource based policies for granting usage permissions.

#### **Learning 3** : Do not over provision a function timeout setting for AWS Lambda Functions

***Max duration of a lambda function is 15 minutes***

*Over provisioning function timeout often results in functions running longer than expected and unexpected costs.*

> AWS Lambda allocates compute power in proportion to the memory you allocate to your function. This means we can over provision memory to run functions faster and potentially reduce costs. And, AWS recommends that we should not over provision function time out settings. Always understand code performance and set function timeout accordingly. 
> 
> Over provisioning function timeout often results in functions running longer than expected and unexpected costs.

#### Learning 4: Dependencies cannot be packed separately from the actual aws lambda package

***Total size including dependencies and other stuff can be 250MB***

#### Learning 5: AWS Lambda functions can now be deployed as containers 

#links-to-read-for-ssa
*https://aws.amazon.com/blogs/aws/new-for-aws-lambda-container-image-support/*

> you can now package and deploy Lambda functions as **container images** of up to **10 GB** in size.
> 
> functions deployed as container images benefit from the same operational simplicity, automatic scaling, high availability, and native integrations with many services.
> 
> We are providing **base images** for all the supported Lambda runtimes (Python, Node.js, Java, .NET, Go, Ruby) so that you can easily add your code and dependencies. We also have base images for custom runtimes based on [Amazon Linux](https://aws.amazon.com/amazon-linux-2/) that you can extend to include your own runtime implementing the [Lambda Runtime API](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-api.html).
> 
> We are also releasing as open source a [**Lambda Runtime Interface Emulator**](https://github.com/aws/aws-lambda-runtime-interface-emulator/) that enables you to perform local testing of the container image and check that it will run when deployed to Lambda. The Lambda Runtime Interface Emulator is included in all AWS-provided base images and can be used with arbitrary images as well.


#### Learning 5:  Amazon FSx for Lustre has support to temporarily access data from S3 as cold data for quick reads and updates at low cost, while storing "hot data" to be processed locally. Lustre offers high storage and processing speed

*Lustre is for Hight Performance Computing - it needs direct access to the instances for configuration purposes , not very compatible with services like fargate where everything is internally handled within docker containers*

> FSx for Lustre makes it easy and cost-effective to launch and run high performance file systems. Lustre's file system is open sourced and is used for applications that require fast storage that can keep up with compute. 
> 
> Can be linked with S3 buckets and objects will be shown as files in the FSx for Lustre system.
> 
> Similar Services as Lustre:
> - FSx for Windows File Server: Provides a fully maanged highly reliable file storage that is accessible over the SMB ( ServiceMessage Block ) protocol
>   Built onWindows Server, offers, user quotas, end user file restore, Microsoft Active Directory integration. However this does not allow to present S3 objects as files  and therefore cannot access cold data for quick access at low cost
>   
>   - EMR: Industry leading cloud big data platform - processing vast data using Spark, Hive, HBase, Flink, Hudi and Presto. EMR uses Hadoop to distribute data across a cluster of EC2 instances, however does not offer same storage and processing speed as Lustre. 
>     
>    Glue : Fully manaded ETL service makes it easy for customers to prepare and load data for analytics. Menat for batch ETL data processing. Goes not offer processing and storage speed as Lustre.


#### Learning 6: Elasticache for Redis is HIPAA eligible and PCI DSS Compliant. 
#links-to-read-for-ssa
https://aws.amazon.com/elasticache/redis-vs-memcached/

> Elasticache for redis is a blazing fast in-memory data store that provides sub-millisecond latency to power internet scale realitme applications. 
> 
> Both Amazon ElastiCache for Redis and Amazon ElastiCache for Memcached are HIPAA Eligible.
> 
> Amazon ElastiCache for Memcached is a great choice for implementing an in-memory cache to decrease access latency, increase throughput, and ease the load off your relational or NoSQL database. Session stores are easy to create with Amazon ElastiCache for Memcached.


#### Learning 7: Nat gateway does not support port forwarding but NAT INSTANCE does

*Instance supports three feature | NAT Gateway nothing | Gateway easier to set up*

#links-to-read-for-ssa
*https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html*

![[Screenshot 2024-05-23 at 1.45.15 AM.png]]

#### **Learning 8** : AWS S3 Storage class analysis does not give recommendations for transitions to the ONEZONE_IA or S3 Glacier storage classes. It only gives recommendation from Standard to Standard IA

*Storage class analysis only Standard to Standard IA*

> By using sS3 Analytics storage Class analysis you can analyze storage access patterns to help decide when to transition less frequently accessed STANDARD storage to STANDARD_IA. And NOT other classes.
> 
> - On the other hand AWS **Cost Explorer Service** helps you to identify under utilized EC2 instances that may be downsized on an instance by instance basis within the same instance family.
> - **Compute Optimizer service** recommends optimal AWS compute resources for workloads to reduce costs and improve performance. Helps you chose the right instance type based on your utilization data.

#links-to-read-for-ssa 
- [https://aws.amazon.com/compute-optimizer/](https://aws.amazon.com/compute-optimizer/)
- [https://aws.amazon.com/premiumsupport/technology/trusted-advisor/best-practice-checklist/](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/best-practice-checklist/)
- [https://docs.aws.amazon.com/AmazonS3/latest/dev/analytics-storage-class.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/analytics-storage-class.html)
- https://aws.amazon.com/dms/schema-conversion-tool/

#### Learning 9 : When the execution role of AWS Lambda and Amazon S3 bucket are to be accessed from different accounts,

> You need to grant Amazon S3 bucket access permissions to the ***IAM role*** and also ensure that the ***bucket policy*** grants access to the AWS Lambda function's execution role

#### Learning 10: Traffic from an NLB is routed to instances using the primary private IP address specified in the primary network interface for the instance

#### Learning 11: Copying / replicating data across S3 Buckets

*S3 **Transfer Acceleration** is **NOT for copying objects** across S3 Buckets but rather for secure **transfer of files over long distances** between client and S3 bucket.*

*Buckets cannot be copied, but data can be synced | Data sync can be done across accounts \ se copy command can also be used as long as bucket policies are active and roles are provided to the sync service*

>1.  The `aws s3 sync command` uses the CopyObject APIs to copy objects between Amazon S3 buckets. 
> 
> The ***sync command*** lists objects that are in the source but aren't there in the target. It also identifies objects that are in the source and have a different last modified date. 
> 
> The metadata of the objects are preserved, but the ACLs are set to full control to the target account, if any op fails, it can be run again without duplicating previous results

> 2. ***S3 Batch replication*** is a way to replicate objects that existed before a replication configuration was in place. and objects that failed replication. 
>    
>    Objects can be replicated to multiple S3 buckets, in different regions . 

#### Learning 12: Data moving in between an encrypted EBS volume and the EC2 instance is encrypted.

> Encryption operations occur on the servers that host Amazon EC2 instances, ensuring the security of both data-at-rest and data-in-transit between an instance and its attached Amazon EBS storage.

#### **Learning 13** : VPC Peering vs VPC Sharing

Situation: 
 The company has set up AWS Organizations to manage several departments running their AWS accounts and using resources such as Amazon EC2 instances and Amazon RDS databases. The company wants to provide ***shared and centrally-managed VPCs*** to all departments using applications that need a high degree of interconnectivity.

> **VPC Sharing** : Allows multiple AWS Accounts to create their application resources such as EC2 instance, RDS databases, etc.. into a shared and centrally managed VPCs.
> 
> The owner of the VPC shares one or more subnets with other accounts that belong to the participants within the same organization. After the subnet is shared, the participant can view, create, modify and delete their applications in the subnet shared with them. They cannot view, update or delete resources that do not belong to them. 
> 
> We can use shared VPCs to leverage the implicit routing within a VPC for applications that require a high degree of inter connectivity and are within the same trust boundaries. This reduces the number of VPCs while using separate accounts for billing and access control

> **VPC Peering** : Is a networking connection between two VPCs that enable you to route traffic between them using private IPv4 addresses or IPv6 addresses. Instances in either VPC can communicate with each other as if they are within the same network, VPC peering does not facilitate centrally managed VPCs and therefore is an incorrect option.

#links-to-read-for-ssa 
- [https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html)
- [https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)

#### Learning 14: Aurora cluster | Replicas

> Aurora ***replicas*** have two purposes. We can **Increase read capacity** by issuing queries to the reader end point of the cluster.
> 
> If a writer instance becomes un available, Aurora ***automatically promotes one of the reader instances*** to take it's place as the new writer. Upto 15 Aurora Replicas can be distributed across AZs within a Region

#### Learning 15: Cloud Front Points of Presence

> CF is a fast CDN service that securely delivers videos, data, applications ***and APIs*** to customers globally with low latency, high transfer speeds , all within a developer friendly network. 
> 
> POPs - Cloud Front points of presence (edge locations) make sure that popular content can be served quickly to viewers + CF has regional edge caches to bring content closer to viewers even if it is not popular to stay at the POP (Point of presence).
> 

#### Learning 16: AWS Direct Connect helps you establish a dedicated network connection between your network and one of AWS Direct Connect Locations. This connection can be partitioned to multiple Virtual Interfaces (VIFs).

> What is a virtual interface ?
> 
> This does not involve internet, but rather uses a ***dedicated private network connection*** between intranet and amazon VPC. Is this why it takes about a month to set it up ?


#### Learning 17: AWS Global Accelerator is a service that provides static IP addresses that act as a fixed entry point to our application end points in a single or multiple regions such as ALB, NLB, EC2 instanes, ... uses AWS Global Network and it's edge locations around the world to route traffic

*Use global accelerator for not HTTP use cases*

#### Learning 18 : ACM, Certificates and AWS Config Service

*certificates by ACM are auto renewed | Imported ones are not*

> **AWS Config Service** : AWS Config provides a detailed view of the configuration of AWS resources in your AWS account. Let's us see how resources were configured in the past and let's us see how config changed over time.
> 
> ***CERTIFICATES CREATED IN ACM ARE AUTOMATICALLY RENEWED***
> 
> *ACM DOES **NOT** AUTO-RENEW CERTIFICATES THAT WE **IMPORT***
> 
> We can leverage the `acm-certificate-expiration` check, an AWS-managed rule to check if any ACM certificates are marked for expiration within a specified number of days. We can be notified whenever ***AWS Config*** evaluates custom or managed rules against our resources. 

**Monitoring the `days-to-expiry` AWS Cloud Watch Metric** : It is certainly possible to use the `days to expiry` CloudWatch metric to build a CloudWatch alarm to monitor the imported ACM certificates. The alarm will, in turn trigger a notification to the team. But this option needs more config effort than directly using the AWS config managed service that is available off the shelf.


#### Learning 18: S3, Data Streams, SQS, SNS and Lambda 

Situation: A Big Data analytics company writes data and log files in Amazon S3 buckets. The company now wants to stream the ***existing_data_files*** as well as any ongoing file updates from Amazon S3 to Amazon Kinesis Data Streams.

As a Solutions Architect, which of the following would you suggest as the **fastest possible way** of building a solution for this requirement?
![[Screenshot 2024-05-23 at 4.07.33 PM.png]]

**Database Migration Service can help here**

> ***DMS enables us to seamlessly migrate data*** from supported sources ***to*** RDBMS, warehouses, ***streaming platforms*** and other data stores in the cloud.
> 
> Since we need to implement it in least possible time, DMS can be used. 
> 
> DMS lets us stream data from S3 to Kinesis Streams for real time analytics without any code change. It supports targets such as Kinesis and Amazon Kafka. ***Allows for migration of full and change data capture files.***
> 
> From kinesis several consumers such as Lambda, Firehose, Kinesis Data Analytics and the Kinesis Consumer Library can consume the data concurrently to perform real-time analytics on the dataset. See image above.
> 
> Again here, the other options included using aws Lambda as the middle step to write data to kinesis. However since Lambda would require writing custom functions and some development time, it is not the fastest solution.


#### Learning 19 : Cloud Front vs Global Accelerator

A media company wants a ***low-latency way*** to distribute live sports results which are delivered via a proprietary application using ***UDP protocol***.

As a solutions architect, which of the following solutions would you recommend such that it offers the **BEST performance** for this use case?

Options: Cloud Front or Global Accelerator

> **Correct option - Use Global Accelerator . Why Not cloud front ?**
> 
> Global Accelerator is a networking service that helps **improve availability and *performance* of applications to global users.** (***performance*** is a key word)
> 
> It provides a static IP that provides a fixed entry point to our applications across Regions / AZs. 
> 
> It takes into consideration, application health, user's location and other policies to route users to the right end point of our application. 
> 
> It is a ***good fit for non-HTTP use cases*** such as gaming (UDP), IoT (MQTT) or VoIP. Therefore this is the right choice. 
![[Screenshot 2024-05-24 at 12.53.03 PM.png]]

> **Cloud Front :** Why is this NOT the bests option ?
> 
> Cloud front is a fast CDN service that securely delivers data, videos, applications and APIs to customers globally with low latency. 
> 
> Edge locations make sure that popular content is cached to be served quickly, in addition to Regional Caches. 
> 
> **It supports HTTPS and RTMP protocol based requests and therefore NOT a SUITABLE option for this use case where it is UDP protocol based.** 
> 

Cloud front and Global Accelerator are separate services that use the AWS Global Network and it's edge locations around the world. 

Cloud Front improves performance for both cacheable content and dynamic content such as API and dynamic site delivery.

AWS Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge locations to applications running in more than one AWS Regions. 

Global accelerator is a good fit for NON-HTTP use cases such as gaming (UDP)
, IoT ( MQTT ) or VoIP as well as HTTP use cases that specifically require **Static IP**

#### Learning 20: Launch Configuration vs Launch Template

*LT is new | LT is version-able | LT is recommended | LC is old , LC is immutable*

> We can ONLY USE a LAUNCH TEMPLATE to provision capacity across MULTIPLE INSTANCE TYPES. While we can't do it using a LC
> 
> USE LT as LC is Legacy
> 
> Launch Configurations are immutable: It is not possible to modify a launch configuration once it is created
> 
> **Launch templates** are **mutable** and can be ***versioned*** - ***AWS*** ***recommends Launch Templates***

#### Learning 21 : Replication data from databases to Redshift

*USE DMS*

Situation: The business analytics team at a company has been running ad-hoc queries on Oracle and PostgreSQL services on Amazon RDS to prepare daily reports for senior management. To facilitate the business analytics reporting, the engineering team now wants to ***continuously replicate this data*** and consolidate these **databases** into a **petabyte-scale data warehouse** by **streaming data to Amazon Redshift**.

As a solutions architect, which of the following would you recommend as the ***MOST resource-efficient solution*** that requires the ***LEAST amount of development time** **without*** the need to ***manage the underlying infrastructure***?

Options: Glue, EMR, DMS, Kinesis Data Streams

> **I chose amazon EMR** ? Why because it had the word, petabyte-scale-data
> 
> **WRONG**: EMR involves significant infra management to set up and maintain the EMR cluster. + This option r***equires a major dev effort*** to write custom migration jobs to copy the database into redshift.
> 
> **Glue** ? : Glue is a fully managed ETL service that makes it easy for customers to prepare and load data for analytics. Is meant to be used for batch ETL data processing. 
> 
> **WRONG** : Why ? Glue involves ***significant dev efforts*** to write custom migration scripts to copy the database into Redshift. 
> 
> **Kinesis Data Streams** : 
> **WRONG**
> While kinesis helps with capturing database event streams, the ***user is expected to manually provision and appropriate number of shards*** to process the expected volume of incoming data stream. Hence it is not the right fit for this use case.

**CORRECT** : DMS
![[Screenshot 2024-05-24 at 1.21.52 PM.png]]
> The DMS instance must be located in the same region. It helps us migrate databases to other AWS services quickly and securely. 
> 
> Source database remains fully operational during this migration, minimizing downtime.
> 
> With DMS
> 
> We can ***continuously replicate data with high availability* and consolidate databases into a *petabyte-scale data warehouse*** by streaming data to Redshift and S3.
> 
> How it works: DMS first moves data to S3 bucket. 
> When files reside in S3 bucket, DMS then transfers them to proper tables in the Redshift data warehouse. 

#### Learning 22: Interface End point vs Gateway End point

*Gateway ads on to Route table | For S3 and Dynamo DB*

Both of these are types of VPC End Points: Virtual Private Cloud End Points

What is a VPC end point and why do we need them ?

Several AWS services can be accessed securely from within a VPC without the need for a VPC end point and they typically provide their own mechanisms for secure access and do not require traffic to leave the AWS network or traverse the internet. 

Examples are : RDS, Elasticache, RedShift, ECS, Lambda, SSM, ALB, NLB.

But other services like S3 cannot be placed within a VPC as ***S3 is a global service*** accessible over the internet or via a VPC end point. These VPC end points allow for direct, private connectivity to S3 from within the VPC without using the Public Internet. 


> **Interface End Point** : Elastic Network Interface (ENI) with a private IP address from the IP address range of your subnet that serves as an entry point for traffic destined to a supported service. 
> 
> Basically, the ***Interface End Point is an ENI that sits at the boundary of the subnet in which we have the service***. So traffic can enter that subnet and access that service. 

> **Gateway End point** : Specifically for connecting to S3 and DynamoDB. This creates a gateway route in your route table, directing traffic for these services through the end point.
> 
> **Why Gateway end point for these service.** 
> 
> 1. Gateway Endpoints provide a highly efficient and scalable way to route traffic directly within the AWS network, bypassing the need for additional hops that come with Interface end points. 
> 
> 2. Both S3 and DynamoDB handle very high volumes of traffic ***Gateway Endpoints can handle large-scale data transfer without the performance limitations*** that might come with the ENI based architecture of Interface End points. 
>    
>  3. Unlike interface end points, there are ***no additional cost associated with creating and using Gateway End points***


#### Learning 23 : SQS Standard Queues vs FIFO queues

 *Standard queue  can support unlimited throughput for both batch and realtime | Batching done to save number of operations*
 *FIFO queue supports up to 300/s without batching and 3000/s with batching* 

Transitioning form Standard to FIFO queue: 

> Standard queues offer 
> - Max throughput,
> - best-effort-ordering, and 
> - at least once delivery. 
>   
> FIFO queues offer: 
> - Exactly once processing
> - In the exact order the messages were sent
>   
>   FIFO queues support 3000 messages / second **with batching** 
>   and up to 300/second **without**. 
>   
>   The name of a FIFO queue **must end with a `.fifo` suffix**
>   
>   CANNOT CONVERT STANDARD QUEUE TO A FIFO QUEUE. To migrate, we have to make a new FIFO queue and connect to it or delete the existing queue and recreate it as a FIFO queue.

#### Learning 24: Using Cloud Watch Alarms to automatically stop, terminate, reboot and recover EC2 instances

#### Learning 25: We cannot SSH into an RDS database instance. So whenever there is any question about secure database access, it means securing the data in transit. 

*For RDS we can set up SSL for data in transit.*


#### Learning 25: Read Replicas in Aurora

![[Screenshot 2024-05-24 at 2.48.25 PM.png]]

> **Replication in Aurora DB cluster**: 
> 
> - Aurora has one primary DB instance and one or more replica instances and a `clusterVolume` that manages data for these DB instances. 
> - Aurora Cluster volume is a virtual database storage volume that spans multiple AZs and each AZ has a copy of the cluster data.

> **Types of instances in a Aurora DB cluster** : 
> 
> **Primary Instance** : Supports both read and write. Each aurora cluster has one primary connected through a write end point
> 
> **Aurora Replicas** : Each Aurora cluster can have upto 15 aurora replicas in addition to primary DB instance. 
> - These replicas serve as a failover and become the primary instance
> - We can scale read operations by pointing all read queries to the reader end point.


**YOU CANNOT PROVISION ANOTHER AURORA DATABASE AND THEN LINK IT AS A READ REPLICA FOR THE PRIMARY DATABASE**

All read replicas are present within the existing DB cluster.

**THERE IS NO CONCEPT OF STANDBY INSTANCE IN CASE OF AURORA.** **STANDBY INSTANCES ARE A FEATURE OF AMAZON RDS while Setting up MULTI AZ DEPLOYMENT**- Standby instance will be in another AZ and be made primary when there is AZ failure. Standby instance is not to be used as read replica. Standby instance has synchronous replication with the primary.

When the main DB instance fails, the standby instance kicks in and traffic is redirected there.

Creating a read replica - RDS takes a snapshot of the source instance and cretes a read-only instance form the snapshot. Unlike a read replica a stand-by replica cannot serve read traffic. There is synchronous replication of data from the primary to the standby replica. This is for disaster recovery purposes. Clients can still read data only from the primary or the read replicas.

#### Learning 26: Bootstrapping AWS Instances

Situation: Your company is deploying a website running on AWS Elastic Beanstalk. The website takes over 45 minutes for the installation and ***contains both static as well as dynamic files that must be generated during the installation process***.

As a Solutions Architect, you would like to ***bring the time*** to create a new instance in your AWS Elastic Beanstalk deployment to be ***less than 2 minutes.*** Which of the following options should be combined to build a solution for this requirement? (Select two)

**Speeding up deployment times**

> 1. Providing  Golden AMIs that already come with pre installed software that just need to be run once the image boots up
>    
>  2. Like how we did in cloud computing course, we can harden the AMI and just install / create the dynamic files during boot time. Like for example: creating an environment file during boot time to hold values like credentials and other tokens that can be dynamically generated 
>     
>   3. While you can store static content in Amazon S3, dynamic content cannot be generated, it has to be done within the instance. Hence using S3 is a bad idea to speed up boot time.

#### Learning 27: Minimum storage duration is *30 days* before you can transition objects from S3 Standard to OneZone-IA or Standard IA

#### Learning 28: Services that can be used or buffering or throttling to handle traffic variations

> Throttling is the process of limiting the number of requests and authorized program can submit to a given operation in a given amount of time. 
> 
> **API Gateway** Helps with throttling: Uses the token bucket algorithm. A token counts for a request. It sets a limit on a steady-state rate and a burst of request submissions against all APIs in your account. Burst is the maximum bucket size. Above which requests can't be served. 
> 
> **SQS can help with spikes** : SQS offers buffer capabilities to smooth out temp volume spikes without losing messages or increasing the latency
> 
> **Kinesis** : Is a fully managed, scalable service that can ingest, **buffer** and process streaming data in real-time


#### Learning 29: Sources of Amazon *Guard Duty*

> **Guard Duty only monitors these logs**
> 
> - [AWS CloudTrail event logs](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html#guardduty_cloudtrail)
> - [AWS CloudTrail management events](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html#guardduty_controlplane)
> - [VPC Flow Logs](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html#guardduty_vpc)
> - [DNS logs](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html#guardduty_dns)
> 
> Cloud Trail ( Event logs, Management events )
> VPC Flow logs
> DNS logs

#### Learning 30: Pricing Model for AWS Direct Connect

> **Data Transfer Out (DTO)** Refers to the cumulative network traffic that is sent through AWS Direct Connect to destinations outside of AWS. This is charged per gigabyte of data and unlike capacity measurements, DTO refers to the amount of data transferred, not the speed.

#### Learning 31: Testing Blue Green Deployments

> **Blue Green Deployment** : Technique for releasing applications by shifting traffic between two identical environments running different versions of the app. **Blue is the currently running version**. **Green is the new version**. When we are satisfied that the green version is working properly, we can gradually re route the traffic from the old blue environment to the new green environment. 
>
>This can help mitigate risks with deploying new software such as downtime and rollback capability.
>
>**USING ELB**
>If done at a regional level, we can achieve this using an Elastic Load balancer. We can use weighted target groups to specify which target groups to prioritize. However if needed to be done at a global level, an ELB will not work.
>
>**Using Route 53**:
>Weighted routing lets us associate multiple resources with a single domain name and choose how much traffic is routed to each resource. But in cases where DNS caching is present, this will not give any effect as the DNS cache will still have the old IP addresses
>
>**USING GLOBAL ACCELERATOR - This is the RIGHT Choice**:
>In presence of DNS caching and a global deployment, Global Accelerator, helps us ***assign weights to determine the proportion of traffic*** that is directed towards an ***endpoint group*** and traffic dials to control the percentage of traffic that is directed towards an endpoint group ( Region where the app is deployed )

#### Learning 32: Macie and Guard Duty

![[Screenshot 2024-05-24 at 5.18.29 PM.png]]

![[Screenshot 2024-05-24 at 5.18.40 PM.png]]


#### Learning 33: Improving File Upload Speed into S3

> **S3 Transfer Acceleration** : Enables faster and secure transfers of files over long distances between client and an S3 bucket. This takes advantage of Cloud Front edge locations. As data arrives at an edge location, it is routed to S3 over an optimized network path internal to AWS network. 
> 
> **Multi Part Uploads** : 
> - Allows us to upload a single object as a set of parts. Each part is a contiguous portion of the object's data. 
> - We can upload these parts independently and in any order.
> - If transmission of any part fails, just that part can be retransmitted without affecting other parts
> - When object size reaches 100MB, we should consider multipart uploads instead of uploading an object in a single operation
> - Multipart provides improved throughput therefore faster file uploads.

#### Learning 34 : Always prefer Cloud Trail for logging over simpler logging services like S3 Events / S3 access logs - Prefer services that were made for that purpose.

#### Learning 35 : For spread placement group, you can have a maximum of 7 running instances per availability zone per group.





------------------------------------------------------------------------




### Confusions

**Situation**:
You have been hired as a Solutions Architect to advise a company on the various authentication/authorization mechanisms that AWS offers to **authorize an API call within the Amazon API Gateway**. The company would prefer a solution that offers ***built-in user management***.

#### **Difference between Amazon Cognito User Pool vs Identity Pool**

> **User Pool**
	A **user pool** is a user directory in Amazon Cognito. Use to provide ***built-in user management*** or integrate with external identity providers such as Facebook, Twitter, Google+, and Amazon. 

> **Identity Pool**
> 	Provide AWS credentials to grant users access to other AWS services. To enable users in user pool access to AWS resources. We can use identity pool to exchange user pool tokens for AWS credentials. Identity pools aren't an authentication mechanism in themselves.


**Situation** : The engineering team at a company wants to use Amazon Simple Queue Service (Amazon SQS) to decouple components of the underlying application architecture. However, the team is concerned about the VPC-bound components accessing Amazon Simple Queue Service (Amazon SQS) over the ***public internet***.
#### VPC End point vs VPN Connection

> **VPC end point**
> 	AWS Customers can access SQS from within their Amazon VPC using VPC endpoints, without needing to traverse the public internet. VPC end points are powered by ***AWS PrivateLink***, a highly available, scalable tech that enables you to privately connect your VPC to supported AWS services. 
> 	Do not require internet gateway, NAT instance, VPC connection or AWS Direct Connection. Data is transferred within the Amazon network. 
> 	Private Link provides private connectivity between VPCs, AWS services and on-prem applications securely on the AWS network.

> **VPN connection**
> 	VPN connection utilizes IPSec to establish encrypted network connectivity between your intranet (on prem network or any private network outside AWS ) and Amazon VPC ***over the Internet.*** 
> 	
> 	A VPN connection solution can be configured in minutes and is good if we are okay with tolerating the inherent variability in  ***public internet-based connectivity.***


#### VPN Cloud Hub VS AWS Transit Gateway

### Summary of Differences

| Feature          | VPN CloudHub                 | AWS Transit Gateway               |
| ---------------- | ---------------------------- | --------------------------------- |
| **Purpose**      | Simple meshed VPN network    | Scalable, flexible network hub    |
| **Scalability**  | Limited                      | Highly scalable                   |
| **Management**   | Simple setup and management  | Centralized, complex management   |
| **Routing**      | Basic route propagation      | Advanced routing capabilities     |
| **Connectivity** | Remote sites via VPN         | VPCs, VPNs, Direct Connect        |
| **Performance**  | Standard VPN performance     | High performance, low latency     |
| **Cost**         | Cost-effective               | Higher cost                       |
| **Use Case**     | Small to medium-sized setups | Large-scale, complex environments |

### When to Use Which?

- **VPN CloudHub**: Use for simple, cost-effective VPN connectivity between multiple remote sites and a VPC, suitable for small to medium-sized networks with basic needs.
- **AWS Transit Gateway**: Use for large-scale, complex networking requirements where you need to connect multiple VPCs, on-premises networks, and remote sites with advanced routing and segmentation capabilities.

Choosing between AWS VPN CloudHub and AWS Transit Gateway depends on your specific networking requirements, scale, complexity, and budget


#### Virtual Private Gateway

Is a key component to enable connectivity between an AWS Private Cloud and external networks. 

It serves as the anchor on the AWS Side of a VPN connection or a Direct Connect connection.

VPN Connections:
- VGW supports IPsec VPN tunnels allowing us to securely connect on-prem network to AWS VPN over the internet
- Typically 2 tunnels are established for each connection => high availability

Direct Connect:
- Supports direct connect which allows us to establish a dedicated network connection between on-prem data center and AWS
- Higher bandwidth as compared to VPN connections over the internet

AWS Direct Connect and AWS VPN are both used to connect on-premises networks to AWS, but they serve different purposes and offer different features, performance levels, and use cases. Here’s a detailed comparison:

#### DIRECT CONNECT VS VPN
##### AWS Direct Connect

**Purpose**:
- Provides a dedicated, private connection between your on-premises network and AWS.

**Key Features**:
1. **High Bandwidth**: Supports high-bandwidth connections, with speeds ranging from 50 Mbps to 100 Gbps.
2. **Low Latency**: Provides lower latency compared to VPN connections since it is a dedicated physical connection.
3. **Stable Performance**: Offers consistent network performance, unaffected by internet congestion.
4. **Private Connection**: Traffic does not traverse the public internet, enhancing security and privacy.
5. **Direct Integration**: Can be used with AWS services such as Amazon VPC, S3, and others through private virtual interfaces (VIFs).

**Use Cases**:
- Applications requiring high throughput and low latency, such as real-time data processing, large-scale data transfers, and hybrid cloud architectures.
- Ensuring stable and predictable network performance for mission-critical applications.

**Setup**:
- Requires physical installation and configuration of a direct connection from your data center to an AWS Direct Connect location.
- Involves setting up private virtual interfaces (VIFs) and configuring Border Gateway Protocol (BGP) for dynamic routing.

##### AWS VPN Connection

**Purpose**:
- Provides a secure, encrypted connection over the internet between your on-premises network and AWS.

**Key Features**:
1. **Internet-Based**: Utilizes the public internet for connectivity.
2. **Encryption**: Uses IPsec to encrypt data in transit, ensuring secure communication.
3. **Flexibility**: Easier and faster to set up compared to Direct Connect.
4. **Cost-Effective**: Lower initial setup cost compared to Direct Connect, but potentially higher ongoing operational costs due to internet bandwidth charges.
5. **Redundancy**: Supports multiple VPN tunnels for redundancy and high availability.

**Use Cases**:
- Applications that do not require high bandwidth or low latency, such as backup and recovery, occasional data transfers, and secure administrative access.
- Quick and cost-effective way to establish a secure connection to AWS for smaller workloads or testing purposes.

**Setup**:
- Requires setting up a Virtual Private Gateway (VGW) on the AWS side and a Customer Gateway on the on-premises side.
- VPN connection is established over the internet using IPsec tunnels.

##### Comparison Summary

| Feature                      | AWS Direct Connect                         | AWS VPN                                       |
|------------------------------|--------------------------------------------|-----------------------------------------------|
| **Connectivity**             | Dedicated, private connection              | Secure connection over the public internet    |
| **Bandwidth**                | High (up to 100 Gbps)                      | Lower (up to 1.25 Gbps per tunnel)            |
| **Latency**                  | Low                                        | Higher, varies with internet conditions       |
| **Performance**              | Consistent and reliable                    | Variable, depends on internet traffic         |
| **Security**                 | High (private network)                     | High (encrypted traffic)                      |
| **Setup Time**               | Longer (weeks to months)                   | Shorter (hours to days)                       |
| **Cost**                     | Higher initial setup cost, lower ongoing   | Lower initial cost, potential higher ongoing  |
| **Use Cases**                | High-performance, large-scale, critical    | Flexible, cost-effective, less critical       |

##### Choosing Between Direct Connect and VPN

**Use Direct Connect**:
- When you need high bandwidth, low latency, and consistent network performance.
- For applications with stringent performance requirements and large-scale data transfers.
- When privacy and security are paramount, and you prefer to avoid the public internet.

**Use VPN**:
- For smaller, less performance-sensitive applications.
- When you need a quick, flexible, and cost-effective solution.
- For secure administrative access or as a backup to Direct Connect.

##### Hybrid Approach

Many organizations use a hybrid approach, leveraging both Direct Connect for high-performance, critical applications and VPN for flexibility and backup. This ensures they can balance performance, cost, and reliability to meet different workload requirements.