Upto 90% discount compared on On Demand instances.

Two strategies to get a spot instance
- Define your max price and as long as spot price < max defined price, the spot will be available. 
	- Once spot price > max price, there will be a 2 minute grace time to stop or terminate the instance
- Other way is by **Spot Block** (this is a deprecated service in AWS since July 1st 2021 and won't be supported for existing customers from December 2022 ) where we block the spot for a specified period of time 1 - 6 hours without interruptions - in rare cases it may be reclaimed

Looking at the spot pricing history graph we can get to know what would be the cost savings if we were to use spot instances in the longer run
![[Pasted image 20230923221921.png]]

## [[Spot Instance Life Cycle]]