# VPC

An AWS VPC is a component of which AWS family of services : Networking Services

When you launch an instance into a VPC, we provide the instance with a private DNS hostname, and a public DNS hostname
 if the instance receives a public IPv4 address. If domain-name-servers in your DHCP options is set to 
 AmazonProvidedDNS, the public DNS hostname takes the form ec2-public-ipv4-address.compute-1.amazonaws.com for the us-east-1 region, and ec2-public-ipv4-address.region.compute.amazonaws.com for other regions. The private hostname takes the form ip-private-ipv4-address.ec2.internal for the us-east-1 region, and ip-private-ipv4-address.region.compute.internal for other regions. To change these to custom DNS hostnames, you must set domain-name-servers to a custom DNS server.

## VPC Flow logs 

You can create a flow log for a VPC, a subnet, or a NETWORK INTERFACE (not gateways, god damned!)

## VPC Endpoint  

Traffic between your VPC and the other service does not leave the Amazon network.


#### Interface Endpoints (powered by PrivateLink )
An interface endpoint is an elastic network interface with a private IP address that serves as an entry 
point for traffic destined to a supported service. 

A VPC interface endpoint enables you to privately connect your VPC to supported AWS 
services and VPC endpoint services powered by PrivateLink without requiring an
 internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.
  
  Instances in your VPC do not require public IP addresses to communicate with 
  resources in the service.

#### Gateway endpoints (support only Dynamo and S3)
Example: ``

|Destination	|Target|
|---|---|
|10.0.0.0/16|	Local|
|0.0.0.0/0|	igw-1a2b3c4d|
|pl-1a2b3c4d	|vpce-11bb22cc|


The prefix list ID logically represents the range of public IP addresses used by the service. All instances
 in subnets associated with the specified route tables automatically use the endpoint to access the service; 
 subnets that are not associated with the specified route tables do not use the endpoint. This enables you to
  keep resources in other subnets separate from your endpoint.



## Subnets 

 Subnets cannot span availability zones
 
 
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
 

## Limits 

NAT gateways per Availability Zone  <= 5

Per region: 
* Up to 5 VPCs  
* Up to 5 internet gateways  
* Up to 50 customer gateways  
* Up to 50 VPN  
* Up to 200 route tables  
* Up to 5 elastic IP addresses

Up to 500 security groups per VPC

50 rules per security group

5 security groups per network interface 

Up to 200 usbnets per VPC

Up to 5 IPv4 CIDR blocks per VPC

## Route tables 

### Route Table Basics
The following are the basic things that you need to know about route tables:

Your VPC has an implicit router.

Your VPC automatically comes with a main route table that you can modify.

You can create additional custom route tables for your VPC.

Each subnet must be associated with a route table, which controls the routing for the subnet. If you don't explicitly
 associate a subnet with a particular route table, the subnet is implicitly associated with the main route table.

You cannot delete the main route table, but you can replace the main route table with a custom table that you've 
created (so that this table is the default table each new subnet is associated with).

Each route in a table specifies a destination CIDR and a target (for example, traffic destined for the external
 corporate network 172.16.0.0/12 is targeted for the virtual private gateway). We use the most specific route that 
 matches the traffic to determine how to route the traffic.

CIDR blocks for IPv4 and IPv6 are treated separately. For example, a route with a destination CIDR of 0.0.0.0/0 
(all IPv4 addresses) does not automatically include all IPv6 addresses. You must create a route with a destination 
CIDR of ::/0 for all IPv6 addresses.

Every route table contains a local route for communication within the VPC over IPv4. If your VPC has more than one
 IPv4 CIDR block, your route tables contain a local route for each IPv4 CIDR block. If you've associated an IPv6 
 CIDR block with your VPC, your route tables contain a local route for the IPv6 CIDR block. You cannot modify or 
 delete these routes.

When you add an Internet gateway, an egress-only Internet gateway, a virtual private gateway, a NAT device, a 
peering connection, or a VPC endpoint in your VPC, you must update the route table for any subnet that uses these
 gateways or connections.

There is a limit on the number of route tables you can create per VPC, and the number of routes you can add per
route table. For more information, see Amazon VPC Limits.
    

### Main route table 


## Internet Gateway (IG)

 You can't detach internet gateway when somebody use resources in VPC
 
## NAT



### NAT instance

#### Disabling Source/Destination Checks

Each EC2 instance performs source/destination checks by default. This means that the instance must be the source
or destination of any traffic it sends or receives. However, a NAT instance must be able to send and receive 
traffic when the source or destination is not itself. Therefore, you must disable source/destination checks on 
the NAT instance.


## VPC Peering

Communication over IPv6 is not supported for an inter-region VPC peering connection.

## Direct link

AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard 1-gigabit or
 10-gigabit Ethernet fiber-optic cable. One end of the cable is connected to your router, the other to an AWS Direct 
 Connect router. With this connection in place, you can create virtual interfaces directly to public AWS services 
 (for example, to Amazon S3) or to Amazon VPC, bypassing Internet service providers in your network path. An AWS 
 Direct Connect location provides access to AWS in the region with which it is associated, and you can use a single 
 connection in a public region or AWS GovCloud (US) to access public AWS services in all other public regions.
 
 
## Troubleshooting connectivity 

### Troubleshooting Connectivity to EC2i in VPC: 
* Internet gateway for internet access attached
* VPG - virtual private gateway for VPN connection attached, 
* Routing rules from corp network to VPC, in case VPN 
* Routing table on VPC or subnet
* EIP or public IP on instance
* NACLs
* SG
* Os-level firewals