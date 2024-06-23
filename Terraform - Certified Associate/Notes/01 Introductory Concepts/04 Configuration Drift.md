**How to detect config drift ?**
- Compliance tools that can detect mis config - AWS Config
- Built in support for drift detection - AWS Cloud Formation Drift Detection
- Storing expected state - ***tf state files***

**How to correct config drift ?**
- AWS Config
- tf refresh and plan commands
- manually correcting the config ( not recommended )
- tearing down and setting up infra again

**How to prevent config drift**
- **Immutable infra** - Always create and destroy, never reuse
	- Servers are never modified after they are deployed ( Immutable servers )
	- Baking AMI images or containers via AWS Image Builder or HashiCorp Packer
- Using GitOps to version control IaC, and peer review every single change via PRs to the infra 
![[Screenshot 2024-06-18 at 10.51.15 PM.png]]