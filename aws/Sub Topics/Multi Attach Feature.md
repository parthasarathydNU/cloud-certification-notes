- Available in io-1 and io-2 type EBS storages
- This lets, a single EBS volume to be attached to up to 16 EC2 instances on the [[Nitro System]] simultaneously in the same AZ
- Each EC2 instance to which the EBS is attached gets full read write access

#### Key Points
- Suitable for applications that are written to manage and handle simultaneous / parallel Read and Write operations
- Standard [[file systems]] such as XFS or EXT4 cannot be used as a Multi Attach EBS volume because they are not designed for concurrent read/writes on to them
- The file system in the volume has to be cluster based to ensure data resiliency and reliability
- **Cannot be used as boot volumes**

