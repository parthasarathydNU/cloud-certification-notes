Roles help us give specific access to EC2 instances, instead of configuring the credentials within an ec2 instance every time. 
For example this instance here has no Roles associated with it, so when I try to run the command `aws iam list-users` it throws up an error: 
![[Pasted image 20230923185622.png]]

To overcome this, we go to the instance manager and attach a role to this instance that allows it access to iam actions. 

If we check out roles, we see that we have one Demo Role defined, which has the following JSON - here we can see that iam:List* is defined. 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:GenerateCredentialReport",
                "iam:GenerateServiceLastAccessedDetails",
                "iam:Get*",
                "iam:List*",
                "iam:SimulateCustomPolicy",
                "iam:SimulatePrincipalPolicy"
            ],
            "Resource": "*"
        }
    ]
}
```

So we go to instance -> actions -> security -> modify IAM and select the required role for this instance. 
![[Pasted image 20230923190023.png]]

Now if we want to list the users, we are able to see because the role is now attached
![[Pasted image 20230923190139.png]]

	Sometimes it takes a while for IAM roles to propogate to EC2 instances.

