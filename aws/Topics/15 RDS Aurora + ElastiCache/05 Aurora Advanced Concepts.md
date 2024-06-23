### Replica Auto Scaling

![[Screenshot 2024-03-31 at 6.52.06 PM.png]]

### Custom End Points

- Define a subset of Aurora Instances as a custom end point
- Some read replicas are different than the other
- Could be better compute
- Better I/O
- Based on use case

In real world, we will be defining many such custom end points, for many different use cases thereby only querying a subset of our read replicas for each use case.


![[Screenshot 2024-03-31 at 6.54.29 PM.png]]

### Aurora Serverless

Lest manual intervention
- Automated database instantiation and auto scaling based on actual usage
- Good for **infrequent, intermittent or un predictable work loads**
- **No capacity planning** is needed
- Pay per second, can be more cost effective
![[Screenshot 2024-03-31 at 6.56.31 PM.png]]


### Global Aurora

Good for disaster management and recovery
High Availability across regions
Global userbase
Cross region replication less than 1 second, any update in the DB will be available all over the world

- Aurora Cross region **Read replicas**:
	- Useful for disaster recovery
	- Simple to put in place
- Aurora Global **Database**
	- 1 primary region ( read / write )
	- Up to 5 secondary ( read - only ) regions, replication lag is less than 1 second
		- Up to 16 read replicas per secondary region
	- Disaster recovery has a time delay of < 1 minute
	- Typical cross-region replication takes less than 1 sec

Similar to google spanner.

### Aurora Machine Learning

Enables ML based predictions via SQL interface ?? Where will this be used ?

Supported services : Sage Maker and Amazon Comprehend

Use cases: Fraud Detection, Ads Targeting, Sentiment Analysis, Product Recommendation .. 

![[Screenshot 2024-04-02 at 8.35.59 PM.png]]