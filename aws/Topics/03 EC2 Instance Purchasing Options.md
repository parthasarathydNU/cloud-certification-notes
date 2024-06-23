#exam 

There are multiple types of EC2 instances that one can purchase, and let's try to analyze them. 

# Summary
1. **On Demand** - Short term uninterrupted work loads where you can't predict application behavior
2. **Reserved instances** - long term steady state applications like a database
3. **Flexible reserved instances** - long term but attributes can be changed
4. **Savings plan** - Budgeted instances, usage above budget charged at On Demand rate - locked to instance family and region - flexible in size, os and tenancy
5. **[[Spot instances]]** - cheapest, can lose instance any time, fault tolerant, non critical and stateless applications
6. [[04 Tenancy]] - Host, Dedicated, Shared
7. Capacity Reservation - Definitely available on demand at a specific AZ

![[Pasted image 20230923202147.png]]

![[Pasted image 20230923202300.png]]
## EC2 On Demand
- No upfront payment, highest cost `ris:MoneyDollarCircle` `ris:MoneyDollarCircle` `ris:MoneyDollarCircle` `ris:MoneyDollarCircle` `ris:MoneyDollarCircle`
- No long term commitment 
- Recommended for **Short term uninterrupted work loads where you can't predict application behavior**
## EC2 Reserved Instances
- Cheaper as compared on On Demand `ris:MoneyDollarCircle` `ris:MoneyDollarCircle` `ris:MoneyDollarCircle`
- We **reserve a specific instance attributes** - (Instance Type, Tenancy, Region, OS)
- We have a reservation period - One year or three years
- Payment options - no upfront, partial upfront and full upfront
- Reserve the scope - Region or Zone (AZ)
- **Recommended for steady state applications like a database**
- You can buy and sell reserved instance on the Marketplace

## EC2 Flexible Reserved Instances
- Cost more than reserved instances because of flexibility `ris:MoneyDollarCircle` `ris:MoneyDollarCircle` `ris:MoneyDollarCircle` `ris:MoneyDollarCircle`
- Can change all the attributes of the instances that you reserved - OS, Tenancy, Region and Scope ( Region or Zone )

## EC2 Savings Plan
- Same discount as Reserved Instances `ris:MoneyDollarCircle` `ris:MoneyDollarCircle`
- Here we commit to a certain usage limit Eg: 10$ / hr
  Any usage above 10$/hr is billed as an On Demand Instance
- The users are locked to Instance Class-family and Region Eg: M5 (M class family 5) and us-east-1
- Flexibility is in terms of instance size, os and [[04 Tenancy]] 

## EC2 Spot Instance
- **MOST COST EFFICIENT INSTANCES IN AWS** `ris:MoneyDollarCircle`
- These are instances that you can lose anytime if your max price is less than the spot price
- These are spare resources that are made available, but can be reclaimed by other jobs which have a higher priority like the onDemand, or Reserved instance or the Savings Plan
- Recommended for **Fault tolerant tasks, Stateless tasks and Time Flexible tasks **  
- Batch jobs, data analysis, distributed computing, Image processing
- **Not suitable for Databases or Critical tasks** 


## [[04 Tenancy]]

## Capacity Reservations
- Reserve **On-Demand EC2 capacity for any duration** in any **region**
- Paid for even if not used 
- Create or cancel any time ( no billing discounts )
- Charged at on-demand rate
- Recommended for **Short term uninterrupted work loads in a specific AZ**