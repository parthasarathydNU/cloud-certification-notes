Application can handle a greater load by adapting.

Two kinds - vertical & horizontal ( elasticity ).

### Vertical scalability
- Common when we have a non distributed system like a database. 
- Limit to how much we can scale which is a hardware limit
- RDS and ElastiCache are services that can scale vertically

### Horizontal Scalability
Increase the number of instances / systems for the application. 
- Implies distributed systems
### High Availability
- Running application in at least two AZs.
- Goal is to ensure survival of operation even if one data center goes down

High Availability can be passive - RDS Multi AZ for example
Active High availability - horizontal scaling for example.
## High Availability and Scaling for EC2

### Vertical : Increase instance size
- Min t2.nano 
- Max u-I2tbl.metal

### Horizontal - Increase the number of instances
- Auto scaling group
- Load balancer

### High Availability - run instances for same app across multi AZ
- Auto Scaling Group multi AZ
- Load Balancer multi AZ

