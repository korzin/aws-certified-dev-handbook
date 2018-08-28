# Identity Access Management (IAM)

## Policy 

You can use the IAM Policy Simulator to test and validate the effects 
of your IAM access control policies.

## NAT 

### NAT Gateway

A NAT gateway supports bursts of up to 10 Gbps of bandwidth. 
If you require more than 10 Gbps bursts, you can distribute the 
workload by splitting your resources into multiple subnets, and 
creating a NAT gateway in each subnet.

### NAT Instance

Each EC2 instance performs source/destination checks by default. 
This means that the instance must be the source or destination of 
any traffic it sends or receives. However, a NAT instance must be able
 to send and receive traffic when the source or destination is not itself.
  Therefore, you must disable source/destination checks on the NAT instance.

## Remember 

Max number of IAM roles, can be created per AWS Account = 250

 MFA-protected API access cannot work for federated users.
 
 
 You can specify a session limit between 15 minutes and 36 hours 
 (for GetFederationToken and GetSessionToken) and between 15 minutes 
 and 12 hours (for AssumeRole* APIs) for federated users to have access to the console.
 
## Hard part

You can configure your SAML 2.0-compliant IdP such as Active Directory 
to permit your federated users to access the AWS Management Console.
 

 
 
 
 
 
 
 
 
 