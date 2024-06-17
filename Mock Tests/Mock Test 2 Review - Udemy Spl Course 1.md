#### Learning 1: Sharing CloudWatch Dashboards

*Safer way is to share dashboards with iam users / user groups rather than roles or create temp creds*

Situation: A company is launching a new application and will display application metrics on an Amazon CloudWatch dashboard. The company’s product manager needs to ***access this dashboard periodically.*** The product manager does not have an AWS account. A solutions architect must provide access to the product manager by following the principle of least privilege.

> Key Words **Access this dashboard periodically**, **Principle of Least Privilege**

>  Option A: Create a sharable link that is only accessible by the company manager's email address: 
>  Here while they receive a temporary link to access the dashboard,
>  
>  **this link needs to be re created every time they want to access the dashboard. Hence this is operationally inefficient.**

#links-to-read-for-ssa
[Share dashboards with individual users using email id](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-dashboard-sharing.html?source=post_page-----5d649a3e850e--------------------------------#share-cloudwatch-dashboard-email-addresses)

> Option B:  Create a new IAM user with only the `CloudWatchReadOnlyAccess` policy attached. And share the dashboard url and login credentials of the IAM user with the manager. 
> 
> This is the best option because, we apply the principle of least privilege and also the manager can periodically access this dashboard till the IAM user is active

#### Learning 2: Attaching SSL certificates to Regional Resources / Global Resources

*us-east1 for global resources, region otherwise*

When to import SSL certificates to the specific regions and when to import an SSL certificate in us-east1 Region (global resources) ?

> **Regional Certificates**:
> Can be used with resources in the same region, example *ELB, API Gateway Regional End points, Elastic Beanstalk* 

> **Global Certificates**: 
> When the SSL/TLS certificate is ***intended for a global AWS service or distribution***
> Certificates imported in us-east-1 (N.Virginia) to be used with global services such as *Cloud Front, Global Accelerator*


#### Learning 3: API Gateway vs API Gateway *End Point*

*Gateway is the managed service | Gateway End point is how you access the service*

> These are two different components related to building and managing APIs using AWS services
> 
> **API Gateway** : 
> Fully managed service provided by AWS that makes it easy for developers to create, publish maintain, monitor and secure APIs at scale. It acts as a front door for applications to access data and functionality from backend services such as apps running on EC2, Lambda or any web application. 
> 
> Features:
> - Define REST APIs and WebSocket APIs
> - Create, Update, Delete and Update APIs
> - Mapping templates for transforming request and response data
> - Authentication and authorization using IAM roles, Congnito and API keys
> - Request throttling and quotas to protect backend services from being overwhelmed
> - CloudWatch integration for monitoring API usage and performance
> - Detailed metrics for logging API calls
> 
> 
> **API Gateway *End Points***:
> - Refers to specific entry points that clients can use to interact with API hosted on Amazon API Gateway. 
> - End points are the **URLs where the API hosted on Gateway is accessible**
>   
> - REGIONAL END POINTS
> - EDGE OPTIMIZED END POINTS : Deployed globally using Cloudfront CDN to optimize requests from geographically diverse clients
> - PRIVATE Endpoints : Only accessible within VPC using AWS PrivateLink

#### Learning 4: S3 Intelligent-Tiering vs Lifecycle Policies

*Intelligent tiering only standard and IA | Use lifecycle otherwise | Minimum 30 days before transition* 

> **Intelligent Tiering :**
> - Auto optimize storage costs by moving data between **TWO** access tiers: ***Frequent (Standard) Access and Infrequent access***
> - Ideal for data with unpredictable access patterns
> - Infrequent access tier: Optimized for data that is accessed less frequently but requires rapid access when needed

> **Lifecycle Configuration** :
> - Auto transition to different storage classes and expiration / deletion of objects after a specific period
> - ***Rule based transition***
> - ***All storage classes***, Standard, Intelligent tier, Standard IA, One Zone IA, Glacier Instant Retrieval, Glacier Flexible Retrieval, Glacier Deep Archive

#### Learning 5: Controlling access to AWS resources using the AWS organization of IAM principals

*One check for entire organization - accounts, users, every request PrincipalOrgID*

> **Features of Organizations :**
> 
> - **Organizational Units (OUs)** : ***Group accounts into OUs*** to apply policies at different levels
> - **Service Control Policies (SCPs)** : Apply policies at organization, OU or account level, that control the services and actions that can be used across your accounts.- Allow or deny services and actions
> - They affect all IAM users and roles within the account or an OU

>**PrincipalOrgID**:
>
>- A condition key that we can use in IAM policies to restrict access to AWS resources based on Org ID of the principal making the request. 

Example:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::example-bucket/*",
      "Condition": {
        "StringEquals": {
          "aws:PrincipalOrgID": "o-xxxxxxxxxx"
        }
      }
    }
  ]
}

```

#### Learning 6: Various ML and AI services in AWS

*Sagemaker - Entire Studio for ML tasks | Comprehend - NLP | Rekognition - Image Video | Polly - Text to speech | Translate - Text to text | Transcribe - Speech to text | Kendra -  Storage | Textract - extraction | Personalize | Forecase*

##### SageMaker Suite

> **SageMaker :** ML service to build, train, tune, deploy and monitor models
> 
> **SageMaker GroundTruth** : ***Data Labeling service*** that uses ML that support both automated and human in the loop workflows for labeling
> 
> **SageMaker Studio**: All in one tool for Machine Learning Tasks

##### AI Services

> **Comprehend :** NLP Service - text analysis to extract insights, sentiment, key phrases, entities and language ( customer feedback, social media posts, or any text data) | Comprehends **text** data | Identify PHI ( Protected Health Information )
> **Textract** : Text extraction from documents | Process invoices, receipts and forms | Content extraction from textual data
> 
> **Rekognition** : Image and video analysis | Object Detection, Feature recognition, content moderation | **Image and video** search . verification and content moderation
> 
> **Polly** : Text to speech service | **Polyglot** - one who can speak many languages | converts text to natural sounding speech
> 
> **Transcribe** : Speech-to-text service | Speech to text 
> 
> **Translate** : Neural machine translation service | Language Translation for Text
> 
> **Personalize** : Recommendations | Personalized experiences
> 
> **Forecast** : Time series forecasting service | Financial forecasting
> 
> **Kendra :** Enterprise, search and knowledge management


#### Learning 7: Even dynamic content can be streamed through cloud front and Global Accelerator is better for non HTTP cases such as TCP and UDP

Reference : [Deliver Content Faster with Cloud Front](https://aws.amazon.com/getting-started/hands-on/deliver-content-faster/?source=post_page-----fc19cdc39397--------------------------------)

> Cloud Front fetches content from the **origin** such as S3, EC2 instance, ELB or our own web server when it is not already present in the edge location
> 
> CloudFront can be used to deliver entire web app, including ***dynamic, static streaming and interactive content***
> 
> CloudFront is a content delivery network (CDN) service that securely delivers data, **videos**, applications, and **APIs** to customers globally with low latency and high transfer speeds.
> 
> **Dynamic Content Caching** : 
> Reduce load on the origin servers and speed up delivery of frequently listed content
> 
> **API Acceleration** : API responses an be cached reducing latency
> 
> **Web Apps** : Dynamic Web applications can benefit from CFs global network ensuring fast load times for dynamic content generated by backend servers
> 
> **Real Time Streaming :**  CloudFront supports protocols like web socket for realtime bi-directional communication enabling dynamic content delivery in real time applications

**Dynamic Content Caching in Cloud Front**

> - Configure the origin to point to the dynamic content source
> - Enable caching based on query strings, headers
> - **Customize TTL** to control how long dynamic content is cached

**Real-Time Data Streaming with Cloud Front**

**On Demand Streaming**
> - Store audio . video files in S3 or origin server
> - CF caches these files at edge locations
> - Supports HTTP Live Streaming (HLS), Dynamic Adaptive Streaming over HTTP  (DASH)


**Live Streaming**
> - Ingest : Use Elemental MediaLive to encode live video streams and store live video fragments in S3 as the origin
>  - CF Caches live video fragments and delivers them to viewers in realtime
>  - Support HLS and DASH


#### Learning 8: AWS Systems Manager - Recap

*Patch | Run | Scheduled Maintenance*

> **Systems Manager**:
> Unified management service that provides a suite of tools to automate common tasks. Key components - Patch Manager, Run Command and Maintenance Window
> 
> **Patch Manager :**
> Automate ***security updates patching*** for managed Ec2 instances
> 
> **Run Command :** 
> - Execute administrative tasks and scripts across all EC2 instances without the need for SSH or RDP access.
> - Commands executed securely through IAM roles
>   
> **Maintenance Window :**
> Schedule and automate maintenance tasks on instances during specific time windows. Probably choose off peak hours. 


#### Learning 9: Systems Manager is used for security patches and OS updates, while secrets manager is used to store secrets

#### Learning 10: Multi Region Keys in AWS KMS

> Allows us to replicate and manage cryptographic encryption keys across multiple AWS regions. 
> 
> **Primary Key - Replica Key** : Both keys contain the same material, but exist in different regions
> 
> AWS KMS automatically handles replication, synchronization and rotation of key material and synchronization of key properties across all regions


#### Learning 11: AWS Secrets Manager: 

> Designed to securely store, retrieve and manage secrets such as db credentials, API keys and other sensitive information
> 
> Automatic Secret Rotation according to a defined schedule ensuring secrets are updated regularly without manual intervention
> 
> Supports Multi Region Secrets


#### Learning 12: Recap on AWS SSO Services

**AWS SSO :** 

> Cloud based service that simplifies SSO access to AWS accounts and business applications. 
> 
> Provides integration with Identity Providers  like Microsoft Active Directory and External Identity Providers (IdPs) using SAML 2.0
> 
> Built in dir for managing users, or integrates with AWS Managed Microsoft AD or on-prem AD
> 
> Users can access all their assigned AWS accounts and apps from single user portal

**AWS Directory Service  (***AWS Managed Microsoft AD***) ** :

> Offers options to set up and manage directories in the AWS cloud making it easier to integrate with AD environments.
> 
> ***AWS Managed Microsoft AD*** : 
> 
> - Fully managed AD service compatible with Microsoft AD
> - AWS handles the AD infra management including monitoring backup and recovery
> - Establish trust relationships with existing on-prem AD
> - Use Case: Extend on-prem AD to the cloud

**AD Connector :**

> A directory gateway that allows you to connect your AWS resources with an existing on-prem AD
> 
> **Features :***
> - Acts as a proxy to redirect authentication to on-prem AD
> - Easily integrate AWS services with on-prem AD
> - USE CASE: Utilize on-prem AD credentials for AWS services without deploying additional AD infra in the cloud


**SIMPLE AD :**

> A basic Microsoft AD compatible directory that is powered by SAMBA 4

#### Integrating with AD: 

**Extending On-prem AD to AWS :**
 > - Use AWS Managed Microsoft AD to **create a trust relationship with on-prem AD** enabling seamless integration and centralized identity management
 > - This way we can extend on-prem AD to manage AWS resources and applications while maintaining centralized control
 > ![[Screenshot 2024-06-02 at 2.48.59 PM.png]]
 

**AWS SSO with Active Directory :**
- Integrate SSO with either on-prem AD or AWS managed AD to provide users with SSO access to AWS accounts and cloud applications. 
- USE case: Employees use their corporate AD credentials to access AWS Management console and business applications
- AWS IAM Identity center is the successor to AWS SSO![[Screenshot 2024-06-02 at 2.53.28 PM.png]]![[Screenshot 2024-06-02 at 2.53.42 PM.png]]

**AD Connector for direct integration: **
- Use AD connector to connect AWS services directly to your on-prem AD without replicating directory data to the cloud

![[Screenshot 2024-06-02 at 2.55.11 PM.png]]

### Summary

**AWS SSO**: Centralized SSO access management for AWS accounts and applications, with integration options for AD. What is AD ?
  
 >  This is more like managing user login for users who want to access multiple AWS accounts, resources and services. We can move this management of usernames and credentials to another service while still routing users through SSO to access various AWS accounts and services. This is done through AD.

- **AWS Managed Microsoft AD**: Fully managed AD service in AWS, compatible with on-premises AD, suitable for extending AD to the cloud.
  
  This is basically the compressed version of SSO, where just the user credentials and details are stored. This can purely be managed within AWS or it can be used as an extension to an on-prem ad by establishing a trust relationship.
  
  Types of trust relationships: 
  - One way outgoing trust: The AWS managed AD only trusts users from the On-Prem managed AD, so this way, users defined in the On-prem AD can access resources in AWS
  - One way in coming trust : The on-prem managed AD trusts users from the AWS-managed AD. This way users defined in the AWS managed AD can access resources that are on-prem
  - Two-way trust: Users defined in both ADs can access resources in both environments
  

- **AD Connector**: Proxy service for integrating AWS resources with on-premises AD, without replicating directory data.
  
  > Acts as a proxy to on-prem AD without need for data replication. It does not establish any form of trust relationships here. AWS resources can be authenticated against on-prem AD

- **Simple AD**: Lightweight, cost-effective AD-compatible directory for basic needs.

- **IAM**: Core service for access management, supports federated access and integration with external IdPs.

#### Learning 13: A two-way trust is required for AWS Enterprise Apps 

> Such as
> - Amazon Chime, 
> - Amazon Connect, 
> - Amazon QuickSight, 
> - AWS IAM Identity Center, 
> - Amazon WorkDocs, 
> - Amazon WorkMail, 
> - Amazon WorkSpaces, 
> - and the AWS Management Console. 
> 
> AWS Managed Microsoft AD must be able to query the users and groups in your self-managed Active Directory.
> 
> Amazon EC2, Amazon RDS, and Amazon FSx will work with either a one-way or two-way trust.


#### Learning 14: Inspecting and Filtering Traffic that flows in and out of production VPC

*Filtering network traffic using AWS network Firewall*

> We can filter network traffic at the perimeter of VPC using AWS network firewall. This is a stateful, managed, network firewall and intrusion detection and  prevention service.
> 
> How this works: A firewall connects a firewall policy's network traffic filtering behavior to the VPC. This includes specifications for the AZs and subnets where the firewall end points are placed. 

**Traffic Mirroring** - not suitable if the ask is to filter traffic flowing in and out of a VPC

> Traffic mirroring is an Amazon VPC feature that we can use to copy network traffic from an ENI of type `interface`. 
> 
> The mirrored traffic can be sent to an out-of-band security and monitoring appliance for content insepction, threat monitoring and troubleshooting
> 
> These appliances can be deployed as  instances behind a Network Load Balancer or a GWLB with a UDP listener. Traffic Mirroring supports filters and packet truncation so that we can extract only the traffic of interest using monitoring tools of our choice. 

#### Learning 15: Restoring EBS snapshots to *instance store* volumes is NOT_SUPPORTED process.

#### Learning 16: EBS *Fast Snapshot-Restore* F-S-R Feature 

*Turn it on the particular snapshot*
[Amazon EBS fast snapshot restore](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-fast-snapshot-restore.html?source=post_page-----fc19cdc39397--------------------------------)

> Amazon EBS fast snapshot restore (FSR) feature enables you to create a volume from a snapshot that is fully initialized at creation. 
> 
> - This eliminates the latency of I/O operations on a block when it is accessed for the first time
> - Volumes that are created using fast snapshot restore (FSR) instantly delivery all of their provisioned performance. 
> - This has to be manually enabled on each snapshot for which we want the fast snapshot restore to be enabled


#### Learning 17: DynamoDB does not support rules to process data upon write

#### Learning 18: DynamoDB streams

> Capture time-ordered sequence of item-level modifications in any DynamoDB table and store this information in a log for up t 24 hours. 
> 
> DDB Streams writes stream records in near-real time so that you can build applications that consume these streams and take actions based on the contents.

#### Learning 19: AWS Global Condition Context Keys

*Information gathered as the header for requests that go to AWS Services*

> When a `principal` makes a request to AWS, AWS gathers the `request information` into a `request context`.
> 
> You can use the `Condition` element of a JSON policy to compare keys in the request context with the key values that you specify in the policy.
> 
> Request information is provided by different sources: 
> - principal making the request, 
> - resource the request is made against 
> - metadata about the request itself

Properties if the principal: 

> These conditional keys can be used to compare details about the principal making the request against the principal properties that we specify in the policy. 
> `aws:PrincipalArn, aws:PrincipalAccount, aws:PrincipalOrgPaths, aws:PrincipalOrgId...`


#### Lesson 20: IAM Policies vs IAM Roles

*Policy apply on resources | Roles apply on services to access resources - temporary permissions*

Policy: 

> IAM Policy is a JSON document that defines permissions, specifies what actions are allowed or denied for a particular user, group or role

Role: 

> An entity within AWS that can assume permissions through temporary security credentials. It is used to delegate access to AWS resources
> 
> Roles provide temporary security credentials to the entities that assume them, allowing those entities to perform actions defined by the role’s permissions policies.

### Key Differences

| Feature              | IAM Policy                            | IAM Role                                              |
| -------------------- | ------------------------------------- | ----------------------------------------------------- |
| **Purpose**          | Define permissions for actions on AWS | Provide temporary access to AWS resources             |
| **Attachment**       | Attached to users, groups, or roles   | Assumed by trusted entities (users, services)         |
| **Persistence**      | Permanent and reusable                | Provides temporary credentials                        |
| **Common Use Cases** | Managing permissions                  | Cross-account access, service roles, federated access |
### Key Differences

| Feature         | IAM User                                        | IAM Group                                             |
| --------------- | ----------------------------------------------- | ----------------------------------------------------- |
| **Purpose**     | Represents an individual user or service        | Represents a collection of IAM users                  |
| **Credentials** | Has its own username, password, and access keys | Does not have credentials                             |
| **Permissions** | Directly attached policies                      | Policies attached to the group, inherited by users    |
| **Management**  | Managed individually                            | Manages permissions for multiple users collectively   |
| **Use Case**    | Individual access control                       | Simplifying permissions management for multiple users |

#### Lesson 21: Aurora Autoscaling

> - ***Aurora Auto Scaling automatically adjusts the number of Aurora Replicas*** ( Reader DB instances ) provisioned for an Aurora DB cluster ( Each Aurora cluster can have up to 15 replicas ( reader instance ) )
> - Helps DB cluster to handle sudden increases in connectivity or workload
> - When the workload ***decreases***, Aurora Auto Scaling ***removes unnecessary Replicas*** so we don't pay for unused provisioned DB instances


#### Lesson 22: you can share Amazon QuickSight DBs to individual IAM users and groups like how we share files and folders in google drive![[Screenshot 2024-06-02 at 7.27.30 PM.png]]

> Sharing it to the appropriate IAM role would be a possible choice, but it is an added complexity because when we know who are the users that we want to share it to, it is easier to share it with an IAM user rather than a role because roles of users might change, and we might have to assign that role to a user if they have to access it.


#### Lesson 23: AWS Cost Explorer

> This service helps us custom reports that analyze cost and usage data. 
> We can analyze data at a high level, or dive deeper into our costs and usage data to identify trends, pinpoint cost drivers and detect anomalies.

#### Lesson 24: S3 File Gateway

> This service seamlessly conects on-prem applications to the cloud to store and access archive repositories, application data and database backups as durables objects in Amazon S3. 
> 
> S3 File gateway is used for on-prem data intensive applications that need file protocol to access objects in S3![[Screenshot 2024-06-02 at 7.45.33 PM.png]]


### Lesson 26 - Recap what is AWS Shield vs Guard Duty vs Amazon Inspector 

- *Shield* - DDOS, layer 4 / 3
- *Guard Duty* - VPC Flow Logs, DNS Logs, Cloud Watch metrics
- *Inspector* - Run assessment based on assessment template and go through provided recommendation in order of security risk level