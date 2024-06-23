Tenancy refers to how hardware is used to support EC2 instances. 

Tenancy is split into three types - Host, Dedicated and Default / Shared

In simple terms: 

### Host
#### Get access to the physical server itself and we get visibility into the lower level hardware
Host means, an entire piece of hardware is associated with a particular EC2 instance and all the resources of that hardware are fully made available for that instance to use. `fas:DollarSign` `fas:DollarSign` `fas:DollarSign`
- Allows us to address compliance requirements for softwares that use **per-socket, per-core and per-VM licenses**
- Payment options
	- On demand - pay per usage
	- Reserved usage 1 or 3 years (no upfront, partial or full upfront payment)
- For software that has **BYOL** (Bring your own license model) 
- Companies that have strong regulatory needs

## Dedicated
Multiple EC2 instances can use the same hardware, but the hardware is reserved for just one AWS account and other accounts cannot have access to that hardware. Dedicated instances can be used cases that have tenancy restrictions due to security and other compliance restriction. 


# Default
This is the default option, where a particular hardware is shared between multiple instances and can also be used by instances of multiple accounts. 




## Reference image

![[Pasted image 20230923201059.png]]