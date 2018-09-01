
# Elastic Load Balancer 

Multiple certificates only for Application ELB and only since 2017. 

By default, Elastic Load Balancing sets the idle timeout to 60 seconds for both connections. 

Elastic Load Balancing distributes incoming application or network traffic across 
multiple targets, such as Amazon EC2 instances, containers, and IP addresses, 
in multiple Availability Zones.

A load balancer distributes workloads across multiple compute resources, such as virtual servers.
 Using a load balancer increases the availability and fault tolerance of your applications.
 
A load balancer distributes workloads across multiple compute resources, such as virtual servers. 
Using a load balancer increases the availability and fault tolerance of your applications.
 
## Cross-zone balancing 
### AELB 
With Application Load Balancers, cross-zone load balancing is always enabled.
### NELB
With Network Load Balancers, cross-zone load balancing is disabled
 by default. After you create a Network Load Balancer, 
 you can enable or disable cross-zone load balancing at any time.
### CELB

 The following ports are supported: 25, 80, 443, 465, 587, 1024-65535

When you create a Classic Load Balancer, the default for 
cross-zone load balancing depends on how you create the load balancer. 

Cross-zone load balancing reduces the need to maintain equivalent numbers of instances in each enabled Availability Zone, and improves your application's ability to handle the loss of one or more instances. However, we still recommend that you maintain approximately equivalent numbers of instances in each enabled Availability Zone for higher fault tolerance.

## Health checks 

Health checks do not support WebSockets.

### Health Checks for Your Target Groups 

### Configure Health Checks for Your Classic Load Balancer



## Classic Load balancer 

HealthCheck Interval:  30s
Wait for response of health check request : 5s

### Internet-facing CELB

When your load balancer is created, it receives a public DNS name that clients
can use to send requests. The DNS servers resolve the DNS name of your load
balancer to the public IP addresses of the load balancer nodes for your load
balancer. Each load balancer node is connected to the back-end instances using 
private IP addresses.

PUBLIC DNS: 

        name-1234567890.region.elb.amazonaws.com

### Internal CELB

When you create a load balancer in a VPC, you must choose whether 
to make it an internal load balancer or an Internet-facing load 
balancer.

The nodes of an internal load balancer have only private IP
addresses. The DNS name of an internal load balancer is
publicly resolvable to the private IP addresses of the nodes.
Therefore, internal load balancers can only route requests 
from clients with access to the VPC for the load balancer.

PUBLIC DNS (in spite of its 'internal' elb): 

       internal-name-123456789.region.elb.amazonaws.com


### Connection draining for CELB 

To ensure that a Classic Load Balancer stops sending requests
to instances that are de-registering or unhealthy, while keeping
the existing connections open, use connection draining. This 
enables the load balancer to complete in-flight requests made 
to instances that are de-registering or unhealthy.

### Supported protocols by CELB 

Elastic Load Balancing supports the following protocols:
* HTTP/HTTPS
* TCP
* SSL (secure TCP)

### HEADERS (not only for CELB)

#### X-Forwarded-For

The X-Forwarded-For request header helps you identify the IP address of a client when you use an HTTP or HTTPS load balancer.
#### X-Forwarded-Proto
The X-Forwarded-Proto request header helps you identify the protocol (HTTP or HTTPS) that a client used to connect to your load balancer.

#### X-Forwarded-Port
The X-Forwarded-Port request header helps you identify the port that the client used to connect to the load balancer.

















