What is block level storage? : https://aws.amazon.com/what-is/block-storage/#:~:text=Block%20storage%20is%20technology%20that,for%20fast%20access%20and%20retrieval.

[[Block Storage]]
[How to make an attached EBS volume available for use in an EC2 instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html)
[[Multi Attach Feature]]

- EBS volumes are bound by specific AZ
- Multiple EBS volumes can be attached to the same EC2 instance
- Block storage is not a hard drive attached to the physical hardware, but it is a network drive - attached through the same network - hence the latency 

**EBS Snapshots:**
- A backup of an EBS volume at any point in time
- It is recommended to detach a volume while taking a snapshot
- Snapshots can be copied across Regions or AZs

**EBS Snapshot Archive:**
- In case we don't want to immediately use a snapshot, it can be moved to an archive tier that is 75% cheaper
- It takes anywhere within 24 to 72 hours to restore the snapshot in that instance, it is very slow

**Recycle bin for EBS snapshots:**
- Recycle bins can be set for EBS snapshots, to provide a safety net against accidental deletion 
- The retention policy can be set for any time from 1 day to 1 year

**Fast Snapshot restore:**
- Forces a full initialization of the snapshot with very low latency
- This is particularly useful when initializing an EBS or an EC2 instance out of it
- It costs a lot of money to to be used only when necessary

### [[EBS Categories]] (6)
- General purpose: gp2 / gp3 (SSD) (2) - Boot supported
- IO intensive - low latency - mission critical: io 1 / io 2 (SSD) (2) - Boot supported
- Low cost HDD - frequently accessed high throughput workloads: st 1 (1) - Not BOOT
- Lowest cost HDD - least frequently accessed workloads:  sc 1 (1) - Not BOOT
#exam
Only gp2/gp3/io1/io2 can be used as boot volumes


Quiz:

1. You have launched an EC2 instance with two EBS volumes, Root volume type and the other EBS volume type to store the data. A month later you are planning to terminate the EC2 instance. What's the default behavior that will happen to each EBS volume?

		a. Both the root volume type and the EBS volume type will be deleted
		b. The root volume type will be deleted and the EBS will not be deleted
		c. The root volume type will not be deleted and the EBS volume type will be deleted
		d. Both the root volume type and the EBS volume type will not be deleted

	Answer: The root volume type will be deleted and the EBS will not be deleted. By default, the Root volume type will be deleted as its "Delete On Termination" attribute checked by default. Any other EBS volume types will not be deleted as its "Delete On Termination" attribute disabled by default.

	Question 4:
	![[Screenshot 2024-03-21 at 12.43.24 PM.png]]
	# [Why can't I use the new st1/sc1 EBS volumes by AWS as root volumes](https://stackoverflow.com/questions/36735286/why-cant-i-use-the-new-st1-sc1-ebs-volumes-by-aws-as-root-volumes) ?

	https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html
	Throughput optimized (st1) and Cold HDD (sc1) are HDD-backed volumes that are optimized for large streaming workloads where the dominant performance attribute is throughput and not IOPS. **They do not support boot volumes.**

	**Previous Generation Volumes** : Magnetic (standard) volumes 
	They are suited for workloads with small datasets where data is accessed infrequently and performance is not of primary importance. They deliver approx 100 IOPS on avg, with burst capability of upto 100s of IOPS. Supports to be used as boot volume

	**Q: What is EBS Multi-Attach ?** ![[Screenshot 2024-03-21 at 12.52.42 PM.png]]
	EBS is bound to a given AZ, snapshots can be taken and EBS can be replicated in other AZs / regions
	
	**Copying the data to a new encrypted volume takes a lot of time, so the best way is to create an encrypted snapshot and create a new EBS volume with the snapshot**![[Screenshot 2024-03-21 at 12.55.30 PM.png]]

	**!!! None of the EBS volume types gp2, gp3, io1 or io2 can offer such an high IOPS of 310,000, so for such high IOPS it is recommended to use the instance store**  Refer [[11 Instance Store]] ![[Screenshot 2024-03-21 at 12.59.26 PM.png]] 