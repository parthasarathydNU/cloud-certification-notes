### Learning 1: Use Storage gateway file gateway *hardware appliance* in cases where NO VIRTUALIZED COMPUTE RESOURCES are available. 

*Use Gateway Hardware Appliance to Make use of storage gateway in situations where you do not have Virtualized Environment*

**Storage Gateway Hardware Appliance**  :

> Available as a hardware appliance adding to the existing support for VMWare ESXi, Microsoft Hyper-V and Amazon EC2. This means you can now make use of storage gateway in situations where you do not have ****Virtualized Environment***, Server-class hardware or IT staff with specialized skills that are needed to manage them.

### Learning 2 : NFS( File Storage / Parent Child ) is NOT COMPATIBLE with block storage

*Network File System (NFS) is a protocol that allows a computer to access files over a network as if they were on its local storage. NFS is commonly used in enterprise environments for sharing directories and files across multiple servers and clients*

vs

*Block storage is a type of storage that manages data as blocks. Each block is an individual piece of data with its own unique identifier, and blocks can be stored wherever it is most efficient.*

> An NFS Volume is a shared logical unit of storage managed by an NFS server and accessed by clients over a network. It allows multiple systems to share and access files seamlessly, providing a convenient solution for distributed file sharing and collaboration in a networked environment.

### Learning 3: SWF Workflow ( Simple Workflow Service ) 

*A fully managed service that helps developers build, run and scale background jobs that have parallel or sequential steps ( Like MuFlow )*

Workflow: 

> Set of activities that must be executed in a specific order to complete a particular job or process. Workflows are defined programmatically, and the service manages the execution and coordination of these workflows

**Activities** :

> Basic building blocks of a workflow - individual tasks that need to be performed
> - Range from simple data validation to processing video files
> - Activities are implemented as worker programs

**Deciders** :

> Special types of programs that control logic of a workflow
> - They make decisions about the flow of execution

**Tasks** : 

> SEF breaks down the work into tasks, which are dispatched to workers for execution
> - Activity task
> - Decision task

**Domains** : 

 > Logical container for related workflows
 
### Learning 4: Using IAM USER CREDENTIALS to perform tasks from within an EC2 instance is a bad idea

**Security Risks** : 

> Storing IAM user credentials on anEC2 instance increases the risk of credential compromise. IAM Roles provide a more secure and automated way to manage credentials

**Credential Management :** 

> Managing and rotating IAM user credentials manually is prone to errors and less efficient than using IAM roles, which AWS manages automatically

### Learning 5 : Configuring Allowed methods on Cloud Front

While setting up cloud front we usually can mention a list of methods that are allowed. 

1 .**Cacheable Methods** : GET and HEAD are cacheable methods
	So when you see the error "The distribution supports only cachable requests" then it means that only HEAD and GET requests are being accepted by the cloud front configuration.

If incase the cloud front configuration was also setup to accept the OPTIONS method, then we would not see this error, but we would see other errors for methods like POST, PUT, PATCH, DELETE 
	- **403 Forbidden**: Indicating that the request method is understood but not allowed by the server.
	- **405 Method Not Allowed**: Indicating that the request method is not permitted for the resource

While is is a usual practice to configure GET and HEAD method, **OPTIONS** requests can also be cached, but it's not common practice to cache them aggressively.

### Learning 6: S3 Buckets

*Though S3 Buckets can be accessed globally, they are physically associated with a region.* 

> 
> All data stored in that bucket physically resides in that region. This helps optimize latency and compliance with regional regulations.

#### S3 Buckets CANNOT BE TRANSFERRED between AWS accounts via an API

> However we can set up policies and permissions to grant access, or we can copy data from one bucket to another bucket, but **we cannot transfer buckets.**

#### You CANNOT HAVE UNLIMITED BUCKETS in AWS per account

> There is a limit to the number of buckets we can create in each AWS account.

#### BUCKET NAMES CAN CONTAIN ALPHANUMERIC CHARACTERS

> Buckets can be named like the following "knowledgehut1234". Here we so both alphabets and numbers. However there are certain rules that have to be followed like starting with a letter and not containing uppercase letters or underscores


### Learning 7: Maximum execution time for SWF tasks and workflows is one year

> The maximum execution time for both individual tasks and entire workflows is one year.


### Learning 8 : Kinesis Data Streams also be used in situations where we need to maintain Order by carefully selecting the partition key and setting the required number of streams 

Situation: A manufacturing company wants to implement predictive maintenance on its machinery equipment. The company will install thousands of IoT sensors that will send data to AWS in real time. A solutions architect is tasked with implementing a solution that will receive events in an ordered manner for each machinery asset and ensure that data is saved for further processing at a later time.

> In the above situation we can see that, there is a requirement to receive events in an ordered manner for each equipment. 

#### Comparison

**Kinesis Data Streams**:
- Best for **high throughput**, low latency, real time data processing where strict ordering and scalability are crucial
- **Ordering of data** can be strictly maintained by creating shards based on the number of IoT devices present and ensuring that each IoT device pushes to a unique shard
- Higher complexity and cost  + requires careful shard management (partitioning key) to avoid Hot Shards

**SQS FIFO Queue** : 
- Best for simple use cases for low to moderate throughput requirement + a need for strict ordering and exactly-once processing
- Simple to set up , low cost, exactly-once processing
- Limited scalability, higher latency and potential complexity in managing many queues based on number of 


### Learning 9 : Whenever the question is about minimizing administrative overhead lean towards a managed service

### Learning 10: CIDR Ranges and values

- Maximum CIDR range that we can create is /16 ( 65534 possible host addresses )
- Minimum CIDR range /31 ( 2 possible host addresses )

Smaller the subnet mask value, bigger the range. 

In AWS subnets can be created with a CIDR range from (smallest) /28 to (largest) /16.

#### General values of CIDR ranges

- Private Networks : 10.0.0.0/24 ( 16 addresses) or 172.16.0.0/20
- Public subnet 192.0.2.0/24 ( small subnet 16 addresses )

While these are the generally advised values, it is completely okay to create a subnet with the range 20.0.0.0/24.

### Learning 11: Data Processings IS NOT EQUAL to Data Analysis / Analytics

- **Kinesis Data Streams** is used for real time data processing
- **Kinesis Data Analytics** is used for real time data analysis using SQL queries in specific

**Kinesis Data Analytics** : 

- Primarily designed for real-time data analysis using SQL
- Requires managing and writing SQL code to perform transformations on streaming data ( adds a layer or complexity unless required )
- KDAnalytics involves additional cost that comes with running SQL queries continuously on the streaming data

### Learning 12: Lambda might NOT be the BEST FIT for high throughput realtime data processing

- **Short lived execution** : Lambda functions are designed for short-lived tasks, with a maximum execution time of about 15 minutes. Real time data processing might require longer
  
- **Event Driven Processing** :  While Lambda is suitable for event driven architectures, it might not be suitable for handling high-throughput, continuous data streams in real time
  
- **Concurrency limits** : Lambda has concurrency limits which can affect its ability to handle high throughput scenarios
  
- **Cold Starts** : Lambda functions can experience latency due to cold starts, which impact the processing time of streaming data, especially if the functions are not frequently invoked

### Lesson 13: WAF vs Shield

| Feature                    | AWS WAF                                                                | AWS Shield                                                                 |
| -------------------------- | ---------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Primary Purpose**        | Web application firewall                                               | DDoS protection                                                            |
| **Layer of Protection**    | Application layer (**Layer 7**)                                        | Network and transport layer (**Layer 3/4**)                                |
| **Types of Protection**    | Protects against common **web exploits** like SQL injection, XSS, etc. | Protects against DDoS attacks                                              |
| **Customization**          | Customizable rules, managed rules, rate-based rules                    | Predefined DDoS protection, advanced in Shield Advanced                    |
| **Managed Service**        | Yes                                                                    | Yes                                                                        |
| **Integration**            | Integrates with CloudFront, ALB, API Gateway                           | Integrates with CloudFront, Route 53, ELB                                  |
| **Operational Overhead**   | Requires rule configuration and management                             | Minimal for Shield Standard, moderate for Shield Advanced                  |
| **Monitoring and Logging** | Detailed logging via CloudWatch or Kinesis                             | Enhanced metrics and reports in Shield Advanced                            |
| **Cost**                   | Pay per use (based on web ACLs, rules, requests)                       | Shield Standard: Free, Shield Advanced: Additional cost                    |
| **24/7 Support**           | No                                                                     | Yes (Shield Advanced)                                                      |
| **Financial Protections**  | No                                                                     | Yes (DDoS cost protection in Shield Advanced)                              |
| **Best For**               | Protecting web applications from common exploits                       | Protecting against large-scale DDoS attacks                                |
| **Ease of Setup**          | Requires configuration of rules and conditions                         | Automatically included for Shield Standard, Shield Advanced requires setup |

### Lesson 14 : During the period of reservation, even on demand instances will be priced at the same cost as the reserved instances if the total capacity and storage falls within the reserved capacity

> Example: If you own three Reserved Instances with the same instance type and Availability Zone, the billing system checks each hour to see how many total instances you have running that match those parameters. If it is three or less, you will be charged the Reserved Instance rate for one extra instance that is running that hour.

### Learning 15: Custom DHCP Option Set

"*Allows changes to DHCP options without requiring instance reconfiguration.*"

Amazon VPC DHCP option set is a set of config parameters for the Dynamic Host Configuration Protocol (DHCP) that allows you to customize the DNS settings for instances in your vpc . 

When you launch an instance in a VPC, it automatically receives a set of DHCP options - we get to override this part using Custom DHCP option set.

> Suppose we have a VPC in which we want instances to use a custom DNS server and a specific domain name. We can create a DHCP option set with our custom DNS server's IP address and the desired domain name and associate this option set with the VPC.
> 
> Now all instances in the VPC will use this specified DNS server and domain name for DNS resolution.

- A VPC can only be associated with one DHCP option set at a time
- Instances rely on DHCP options for DNS resolution, so changes to the option set can impact the network behavior!
### Learning 16: IP Addresses start from the given  IP in the CIDR value

Example: 20.0.0.128/25

	This has a mask of 25 ( 32 - 25 = 7 )
	 => 2^7 IP addresses = 128 IP Addresses starting from 20.0.0.128 
	128 + 128 =
	
	Start =  20.0.0.128 to
	End = 20.0.0.255 ( 256 including the start )

Example: **20.0.0.0/25**:

	/25 means 32 - 25 = 7
	2 pow 7 = 128 IP Addresses
	
	The range of this CIRD Range is from 
	
	20.0.0.0 to  20.0.0.127 ( total 128 IP addresses including 0 )
	
	Therefore these ranges do not over lap
	
	[20.0.0.0,  20.0.0.127]  <--- and --> [20.0.0.128 , 20.0.0.255]

NO OVERLAP
