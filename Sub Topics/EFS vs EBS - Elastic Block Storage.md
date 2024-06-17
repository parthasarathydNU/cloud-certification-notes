#### **EBS** 
- This is attached to one instance at a time (except Io io1/ io2 (very specific use cases))
- **EBS volumes are locked at AZ level**
- For gp2 IO increases with disk size
- For gp3 & io1 onwards, IO can be increased independently of disk size

To migrate EBS across AZ
- Take a snapshot
- Restore EBS in the new AZ from snapshot
- EBS backups use IO and we should not run them when the load on the instance is a lot, this will make it slow

Root EBS volumes get terminated when the instance gets terminated, but this can be disabled 

**EFS** - Network file system

- Goal: To attach it to 100s of EC2 instances across AZS
- Only for Linux instances - POSIX file system
- EFS has higher price point (can use EFS IA for cost savings)
- **Instance store** is physically attached to EC2, so gone if we lose the EC2 instance
