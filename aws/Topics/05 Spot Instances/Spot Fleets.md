#exam 
Spot fleets are an optimized way of requesting spot instances to complete our tasks within price constraints.  **Combination of Spot Instances + Optional On-Demand Instances**

Launch Pool : a combination of instance types, operating systems and Availability Zones
	When there are multiple launch pools made available, a spot fleet will have the option of choosing from multiple launch pools and provide instances to meet the cost and capacity required for the Spot Request. 


#exam 
#### Strategies to select spot instances

- **lowestPrice** - Spot instances are selected from launch pools that have the lowest cost
  *Recommended when we have short duration tasks and we can get high cost efficiency*
- **diversified** - This allows the spot fleet to provide instances from multiple pools, incase instances from one pool becomes unavailable, instances are provided from other pools
  *Recommended for long running and tasks and this option is great for tasks that require high availability* 
- **capacityOptimized** -  spot fleet provides instances from the pool that has the best capacity available within the cost mentioned and for the number of instances requested
- **priceCapacityOptimized** - spot fleet picks spot instances from the pool which has the optimal capacity then if there are multiple pools available, it picks instances from the one which has the lowest cost




