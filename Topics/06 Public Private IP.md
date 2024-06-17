Public IP Addresses can be accessed from the WWW
Private IP addresses can only be accessed within AWS VPN.

Whenever we stop and start an instance, a new Public IP is attached to this instance. To resolve this issue and have a constant Public IP for an EC2 (Elastic Cloud Compute) instance, we can use something called as an **Elastic IP**.

An Elastic IP is a constant IP made available from the pool of available IPs with AWS and it can be attached to a given instance. 

One available an Elastic IP has to be attached to an EC2 instance or it will be charged for so it has to be released back to the pool.




