Managed Relational DB service for dbs that use SQL. 

The following DBs are managed by AWS
1. PostgreSQL
2. MySQL
3. MariaDB
4. Oracle
5. Microsoft SQL Server
6. IBM DB2
7. Aurora

### Why RDS and not set up our own DB server in an EC2 instance ?

RDS is a managed service 
- Automated provisioning OS patching
- Continuous backups and point in time recovery!
- Monitoring Dashboards
- Read replicas for improved read performance
- Multi AZ setup for disaster recovery (DR)
- Maintenance windows for upgrades
- Vertical and Horizontal Scaling
- Backed by EBS (gp2 or io 1)

However we can't SSH into the instances, we will have to access it through the VMs if we want to have a look at underlying data. 

### Features

- Auto scaling - we have to set maximum storage threshold
- Good for applications with unpredictable workloads
- Supports all RDS database engines