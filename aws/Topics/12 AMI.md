Amazon Machine Instance

AMI is an customization of an EC2 instance
- We can add our own software, OS, monitoring tools, etc...
- Provides faster boot and configuration because it comes with prepackaged software

This is similar to a docker container, where we pre build images for software to run on different machines, here we sort of preconfigure the machines that we want to run.
Docker for machines!

QUIZ:
You can use an Amazon Machine Image in N.Virginia Region `us-east` to launch an EC2 instance in any AWS Region: True / False
   
   False: AMIs are built for a specific AWS Region, they're unique for each AWS Region. You can't launch an EC2 instance using an AMI in another AWS Region, but you can copy the AMI to the target AWS Region and then use it to create your EC2 instances.




