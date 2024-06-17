VPC - [[Virtual Private Cloud]]

ENIs are bound to a specific AZ
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html

- A logical component in a VPC that represents a **virtual network card**

An ENI can contain the following
- One public IPv4 addres
- One primary private IPv4 address from the  VPC's subnet and one or more secondary IPv4
- Have one Elastic IP address associated per ENI
- Can have a description
- One or more security groups associated with it

We can create ENIs separately, attach them to EC2 instances or move them to another EC2 instance in case of failures. 

This means, an IP address that is currently being associated with one instance, can now simply point to another instance, this way traffic can be directed to the other instance. This is crazyyy!!!

Whenever we create an EC2 instance, an ENI is automatically generated along with it, it is that ENI that gives the instance the Private IPv4 address. When we delete an instance, the ENI that was auto generated along with it, also get's deleted. 

To avoid this we can create a custom defined ENI, provide it with the actual private IPv4 address that we want to give, and we will have better control on which instance to attach it, to , use it for failover switching to other Instances. 
