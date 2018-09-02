# AWS General information

## Global infrastructure

## Networking (TOUGH PART)

Amazon reserves the first four (4) IP addresses and the last one (1) IP
 address of every subnet for IP networking purposes.
 
 You can set up a VPC with a Private Subnet only and a Hardware VPN 
 Access to deploy a Site to Site link with the cloud. All instances in 
 the cloud can be configured with
  a route table to send traffic to the corporate DC in London.
  
You need to open port UDP 4500 to setup a VPN with a CGW behind a firewall or router.

### SAML 

SAML stands for Security Assertion Markup Language.

The AWS sign-in endpoint for SAML is https://signin.aws.amazon.com/saml

You can configure your SAML 2.0-compliant IdP such as Active Directory 
to permit your federated users to access the AWS Management Console.

## Other 

### Random 

#### HTTP response meanings 

409 - BucketAlreadyExists,InvalidBucketState,BucketNotEmpty,OperationAborted,RestoreAlreadyInProgress

