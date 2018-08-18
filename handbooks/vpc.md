# VPC



## VPC Endpoint 

VPC Endpoints
A VPC endpoint enables you to privately connect your VPC to supported AWS 
services and VPC endpoint services powered by PrivateLink without requiring an
 internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.
  Instances in your VPC do not require public IP addresses to communicate with 
  resources in the service.
 Traffic between your VPC and the other service does not leave the Amazon network.

## Default VPC

#### Default Security group

Your VPC includes a default security group whose initial rules are to deny all inbound traffic, allow all outbound traffic

## VPC Endpoints

A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.

Policy example to allow manage endpoints : 

    {
        "Version": "2012-10-17",
        "Statement":[{
        "Effect":"Allow",
        "Action":"ec2:*VpcEndpoint*",
        "Resource":"*"
        }
      ]
    }
    

### Types of VPV Endpoints 
 * Interface endpoints (powered by AWS PrivateLink, supported by about 20 services)
   
   An interface endpoint is an elastic network interface with a private IP address that serves as an entry point for traffic destined to a supported service.
 
 * Gateway endpoints - ((separate title))
 
#### Gateway endpoints 

 (S3 and DynamoDB)
 
