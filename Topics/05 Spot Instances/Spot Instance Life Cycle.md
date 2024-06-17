#exam
![[Pasted image 20230923223033.png]]

### Lifecycle
1. Spot Request is created
	1. One time request or a persistent request
2. If it is a one-time request, the instances are created and the request cancelled - will no longer be processed
3. If it is a persistent request, every time an instance is interrupted or terminated, new instances are launched based on spot instance configuration once they become available

### Important Note
	Cancelling a spot instance request does not terminate the instances
Even after the spot instance request is complete / cancelled, the instances need to be manually terminated

