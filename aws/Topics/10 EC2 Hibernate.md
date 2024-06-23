Instead of clearing the RAM like how it happens on instance stop or termination, the contents of the RAM are written to an encrypted file and stored in the EBS attached to the instance. 

Hibernate Documentation - https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/instance-hibernate-overview.html

This happens while the instance is in the stopping state, then once the instance is in the stopped state, the instance is shut down and the EBS contains the dump of the RAM

When the instance is started again, the RAM from EBS is dumped back to memory. 

**Use cases:** 
- When we have long running processes
- When we want faster boot up time
- When we don't want to lose application state

[[11 Instance Store]] -  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html

An instance store is the temporary storage that is usually allocated in the physical hard disk associated with the hardware on which the instance is running. This is often used for temporary storage like cache, buffer, scratch data and other temporary information. 

For EC2 hibernate, the root volume must be EBS, it must be encrypted, **it must not be the instance store** and it must be large. 

![[Pasted image 20230927233521.png]]

### **NOTE**

Hibernation is just similar to starting and stopping an instance, but just with the difference that the RAM is stored in the EBS associate with the instance. 

It is best practice for the instance root volume to not be the Instance Store because, it is most likely that when the instance is started from the hibernate state, it is running on a different hardware. So any information on the previous hardware's physical hard disk is no longer accessible. 
