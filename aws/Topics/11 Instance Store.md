- The EC2 instance store is the physical hard disk that is attached the the underlying hardware that the EC2 instance is running on. 
- This physically attached hardware can provide a very large number of I/O OPS as compared to the network attached EBS.
- However we need to be aware that this type of storage is ephemeral - it will no longer be available when the instance is restarted or stopped or terminated
- This can be used in instances where there is caching, buffer data handling, temporary storage etc etc..

