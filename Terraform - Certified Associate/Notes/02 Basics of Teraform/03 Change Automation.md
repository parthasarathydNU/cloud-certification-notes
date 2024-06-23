#### What is change Management ?
A standard approach to apply change, resolve conflicts brought about by change. 

In the context of IaC, ch mgmnt. is the procedure that will be followed when resources are modified and applied via a configuration script. 

This can be thought of the steps that take place when we run `tf apply` or probably the `tf plan` command.

#### What is change automation ?
A way of **automating*** creating a predictable and consistent way of managing a change request 

Automating the change management process ? Maybe

> Terraform uses Change Automation in the form of **Execution Plans** and **Resource Graphs** to apply and review complex **changesets**
> 
> A change set is a collection of commits that represent changes made to a versioning repo. This is not necessarily the GitHub repo, it is the internal state management that is maintained by Terraform to track changes in the infra config.
> 
> Change automation allows us to know exactly what Terraform will change and in what order, avoiding many possible human errors

Example of a `tf apply` command:

![[Screenshot 2024-06-18 at 11.23.45 PM.png]]
........
![[Screenshot 2024-06-18 at 11.24.30 PM.png]]





