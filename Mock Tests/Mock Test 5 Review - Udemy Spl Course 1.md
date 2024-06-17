
### Learning 1 : WAF is integrated in AWS Shield Advanced

*Shield advanced protects from large scale DDoS attacks | WAF is Integrated with Shield Advanced | WAF protects from common web exploits - managed rules can be deployed from AWS Mktplace*

### Learning 2: Shield vs Shield Advanced

Sure, here's a comparison of AWS Shield Standard and AWS Shield Advanced in a tabular format:

| Feature                              | Advanced                                                                          | Standard                                                         |
| ------------------------------------ | --------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Cost**                             | Paid subscription                                                                 | Free                                                             |
| **Availability**                     | Requires subscription                                                             | Automatically available to all AWS customers                     |
| **Protection Level**                 | Enhanced protection against larger and more sophisticated DDoS attacks            | Basic protection against common layer 3 and layer 4 DDoS attacks |
| **DDoS Cost Protection**             | Available to protect against scaling charges due to DDoS attack traffic           | Not available                                                    |
| **Access to AWS DDoS Response Team** | 24/7 access to AWS DDoS Response Team (DRT)                                       | Not available                                                    |
| **Integration with AWS WAF**         | ***Direct integration, with waiving of AWS WAF charges for protected resources*** | Not directly integrated                                          |
| **Support**                          | 24/7 specialized DDoS support                                                     | Standard AWS support                                             |
| **Visibility and Reporting**         | Enhanced visibility and reporting through AWS Firewall Manager                    | Limited visibility and reporting                                 |
| **Use Case**                         | Best for high-risk applications requiring robust protection and support           | Suitable for all AWS customers needing basic protection          |

Certainly! Below is a comparison in tabular format between AWS WAF and AWS Shield Standard, which should clarify their distinct functionalities and typical use cases:

| Feature                      | WAF                                                                                                                                                           | Shield Standard                                                                               |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Primary Function**         | Web Application Firewall                                                                                                                                      | Basic DDoS Protection                                                                         |
| **Protection Focus**         | Protects against web exploits and common vulnerabilities at the application layer. Layer 7 HTTP/HTTPS                                                         | Protects against common network and transport layer DDoS attacks.                             |
| **Customizability**          | Highly customizable; allows users to set custom rules based on IP addresses, HTTP headers, URI strings, SQL injection, and cross-site scripting among others. | Not customizable; ***standard protection is automatically applied to all AWS customers.***    |
| **Cost**                     | Pay-as-you-go pricing based on the number of rules deployed and web requests processed.                                                                       | ***Included for free with AWS*** services.                                                    |
| **Integration**              | Can be associated with Amazon CloudFront distributions, Application Load Balancers (ALB), and Amazon API Gateway.                                             | Automatically protects all AWS services, including EC2, ELB, Amazon CloudFront, and Route 53. |
| **Visibility and Reporting** | Detailed visibility and logging of web traffic, allowing for sophisticated rule configuration and incident response based on patterns in HTTP/S requests.     | Basic DDoS attack visibility and automatic notifications through AWS Shield.                  |
| **Use Case**                 | Ideal for applications requiring custom security measures against targeted web attacks.                                                                       | Suitable for all AWS customers as a first layer of defense against volumetric DDoS attacks.   |

### Learning 3 : Encryption and Keys in AWS

Below is a comparison table of the four main server-side encryption methods provided by Amazon S3:

| Feature / Encryption Method       | SSE-C (Customer-Provided Keys)                                 | SSE-KMS CMK (Customer Master Keys)                          | SSE-KMS (KMS-Managed Keys)                               | SSE-S3 (S3-Managed Keys)                               |
| --------------------------------- | -------------------------------------------------------------- | ----------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------ |
| **Key Management**                | Managed by the customer                                        | Managed by AWS KMS, but customer controls                   | Managed by AWS KMS                                       | Fully managed by AWS                                   |
| **Key Storage**                   | Keys must be provided by the customer                          | Keys stored by AWS, policies set by customer                | Keys stored and managed by AWS                           | Keys stored and managed by AWS                         |
| **Key Rotation**                  | Fully done by customer                                         | Can be optionally controlled by customer                    | AWS-managed                                              | AWS Managed                                            |
| **Control Over Keys**             | Complete control                                               | High (via AWS KMS settings)                                 | Moderate (via AWS KMS)                                   | No control                                             |
| **Audit Trails**                  | No support                                                     | Detailed logging with AWS CloudTrail                        | Detailed logging with AWS CloudTrail                     | Basic access logging                                   |
| **Integration with AWS Services** | Manual integration per API request                             | Seamless integration with additional control and logging    | Seamless integration with additional control and logging | Seamless integration                                   |
| **Cost**                          | No additional AWS cost for key management                      | Charges for KMS usage apply                                 | Charges for KMS usage apply                              | No additional cost for key management                  |
| **Use Case**                      | Users needing full control over keys, typically for compliance | Similar to SSE-KMS but with greater control and audit needs | Users needing detailed audit and integration with AWS    | General use, where key management by AWS is sufficient |
| **Security Level**                | High, as keys are never stored by AWS                          | Maximum security with key usage permissions and audits      | Enhanced security with permissions for key usage         | Basic encryption at rest                               |

This table outlines the different aspects of each encryption method, helping in deciding which one best fits specific needs, especially in terms of key management, security requirements, and compliance with regulations.

### Learning 4: S3 can also be considered where there is requirement for concurrent access

*If application requires file level access for read/write operations, then EFS is a good choice, by if it is simple put/get operations, S3 is ideal.*

*S3 has better integrations with analytics tools*

*AWS services or third party solutions can be implemented to allow file like access from S3*

*EFS is more expensive than S3 per GB at larger scales*  

**There is fine finer line of difference between S3 and EFS**

> S3 is better for longer term data retention - with lifecycle methods and storage class transition, it is highly cost-effective for long-term storage compared to EFS
> 
> S3 can handle high levels of concurrent access in the form of API calls 
> 
> Many model reporting and analytics tools are designed to integrate with S3 directly. So when it comes to reporting and analytics tools, probably pause and think


### Learning 5: FSx For Lustre vs EFS

| Feature                         | Amazon FSx for Lustre                                                                                                                               | Amazon EFS                                                                                                                                                 |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Primary Use Case**            | High-performance workloads, such as HPC, machine learning, media data processing, and financial modeling.                                           | General purpose file storage for a wide range of applications from enterprise applications to media servers.                                               |
| **Performance**                 | Optimized for fast processing with workloads requiring high-throughput and IOPS. Can scale up to hundreds of GB/s and millions of IOPS.             | Provides adequate throughput and latency compared to FSx for Lustre, but sufficient for most general applications. Scales automatically to petabyte-scale. |
| **File System**                 | Lustre – a type of parallel distributed file system, commonly used in large-scale computing environments. HPC                                       | POSIX-compliant file system that works well with Linux-based applications requiring a traditional file system interface.                                   |
| **Pricing**                     | Cost based on provisioned storage and throughput capacity. Typically more expensive due to high-performance capabilities.                           | Pricing based on actual usage, making it more cost-effective for a variety of use cases.                                                                   |
| **Durability and Availability** | Data is stored redundantly across multiple AZs if configured.                                                                                       | Data is stored redundantly across multiple AZs, ensuring high durability and availability.                                                                 |
| **Ease of Setup**               | ***Typically more complex to set up and integrate, especially with services like AWS Fargate, due to its high-performance computing orientation.*** | Simple to set up and integrate with AWS services including AWS Fargate, with ***built-in scaling and management features.***                               |

### Learning 6 : FSx for Lustre is much more difficult to set up with Fargate

- *Lustre requires more manual intervention to ensure compatibility and optimal performance with services like fargate*
- *Lustre is built for compute intensive task rather than a general storage system* 
- *Fargate abstracts most of the underlying infra, making it challenging to achieve the direct control needed for Lustre's optimizations*
- *Ensuring proper network access and configurations between Fargate and FSx for Lustre can be more complex*

### Learning 7: Cloud Trail Data Events vs Management Events

| **Feature**                        | **Data Events**                                                                                                       | **Management Events**                                                                                              |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Definition**                     | Capture ***data access activities*** on specific AWS resources.                                                       | Capture ***management operations performed on resources*** in your AWS account.                                    |
| **Examples of Tracked Operations** | Accessing objects in an S3 bucket, reading data from a DynamoDB table.                                                | Creating a new EC2 instance, modifying an IAM policy, deleting a VPC.                                              |
| **Default Logging**                | Not enabled by default; must be explicitly enabled.                                                                   | Enabled by default; logs most actions except those listed explicitly as not logged.                                |
| **Use Case**                       | Useful for detailed audits of how data is accessed and modified, often needed for compliance and security monitoring. | Useful for tracking and auditing configuration changes and operational activities within the AWS environment.      |
| **Scope of Coverage**              | ***Focuses on the data plane***—interactions that directly involve data manipulation and access.                      | ***Focuses on the control plane***—management of AWS resources and services.                                       |
| **Cost**                           | Incurs additional costs as they are not enabled by default and can generate a large volume of logs.                   | Included in AWS CloudTrail without additional cost, except for extended history.                                   |
| *Storage Impact*                   | *Potentially large volumes of logs depending on the scale of data operations.*                                        | ***Generally smaller in volume*** compared to data events, unless the account has extensive management activities. |

### Learning 8 : `aws:sourceIp` condition relates to the user source ip and not the ip of the resource

![[Screenshot 2024-06-15 at 10.14.04 PM.png]]![[Screenshot 2024-06-15 at 10.14.13 PM.png]]

In this example, the first block allows terminate ec2 instance action for users in the CIRD range 10.100.100.0/24

The second block deny's any action on ec2 instances that are in other regions apart form us-east-1

Therefore in combination, allow terminate ec2 instance for users in 10.100.100.0/24 for instance in us-est-1

### Learning 9 : Max runtime of lambda is 15 minutes not 15 seconds

### Learning 10 : FsX For Windows File System Supports SMB protocol

Apart from which AWS Storage gateway can also be configures as a file gateway to support SMB protocol

### Learning 11: Storage GW vs Data Sync

- **DataSync** : When primary requirement is ***efficient migration of data between on-prem to cloud*** or between AWS services | Ideal for one time migration or continuous, scheduled data operations
- **Storage Gateway** : Primary requirement is to maintain a ***hybrid storage setup***

### Learning 11 : Volume GW vs File GW

- **Volume GW** : SAN Architecture
	- For ***block level data access*** typically required by databases and other apps that interact directly with the storage layer 
	- Use when high performance at block level is critical
	- Compatible with Storage Area Network (SAN) - which provides block level access
  
- **File GW** : NAS Architecture
	- ***File level data access*** where applications require a standard file system interface. 
	- ***Native integration with S3 lifecycle management*** is better with File GW 
	- Optimized for efficient file transfers 
	- Compatible with Network Attached Storage (NAS)

### Learning 12: Whats RAID:

***Redundant Array of Independent Disks***

*RAID configurations are useful in scenarios where the built-in redundancy and resilience of EBS are not sufficient for the user's specific requirements. | AWS Does not inherently provide RAID configuration ridectly, it is up to the user to implement and manage RAID configurations as per their app needs*

Technology that combines multiple physical disks into a single unit for purpose of data redundancy performance or both. 
#### RAID Levels

0 (Stripping - data available in strips that can be parallelly accessed)
- Splits data across multiple disks increasing speed and capacity but no redundancy. If one disk fails, data in that array is lost

1 (Mirroring)
- Duplicates same data on two disks, provides redundancy as data is written identically to two disks

10 ( combination of 1 and 0)
- Has both stripping and mirroring , thereby offering both redundancy and high throughput

