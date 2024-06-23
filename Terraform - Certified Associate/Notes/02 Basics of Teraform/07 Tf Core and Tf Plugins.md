
Terraform is logically split into two main parts: 

**Terraform Core:**
- Uses remote procedure calls to communicate with terraform plugins
  
**Terraform Plugins**:
- Expose an implementation of a specific service or provisioner

![[Screenshot 2024-06-19 at 12.18.01 AM.png]]

### Interaction between tf core and tf plugin

When we run any tf commands, several component of tf interact: 

1. **tf core**: This is the primary component that runs on the local machine. Responsible for reading config files, generating and managing the execution plan, maintaining state and more. It interprets the config files that we have written and figures out the dependency order and determines what needs to be created, updated or deleted. 
2. **tf plugins (Providers) :** These are dynamically loaded when tf runs and are responsible for the actual interaction with the APIs of the service providers like AWS, GCP, Azure etc. By default these plugins run on local machine as sub processes of the main tf process. Tf communicates with these plugins over RPC calls.

Therefore both tf core and tf plugins by default exist and run on our local machine. The "remote" aspect comes into play with the actual API interaction with the cloud services ( handled by the plugins ) and potentially with state management if configured to use a remote backend to save state files.

#### Why RPC ?

Remote Procedure Calls are a powerful technique used in computing to enable a program to cause a procedure ( sub routine ) to execute in another address space ( commonly in another computer on a shared network . RPC abstracts the intricacies of the network by allowing the developer to call procedures on other machines as if they were local to the calling environment. 

- **Call Semantics :** When an RPC is made, the calling environment is blocked while waiting for the result of the remote procedure making it appear as through a local procedure is being executed
- **Client Server Model :** RPC typically follows a client server model where a client sends a request to a server and waits for a response

**Why RPCs when both are running locally ?**

- **Isolation :** Running plugins as separate processes and communicating via RPC allows TF to maintain isolation between the core process and the plugins. This is crucial for stability and security, as issues in plugin won't directly impact the core tf process.
- **Modular :** This architecture makes tf highly modular. Providers can be developed independently of the core tf engine. they can be updated and distributed separately without needing to recompile or even restart terraform
- **Compatibility and versioning :** Different plugins can be built using different technologies or languages as long as they adhere to the RPC interface.