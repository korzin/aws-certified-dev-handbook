# Route 53
 
## Random facts (remember)

You have configured for Route 53 and wish to configure failover options for your webservers. 
 What is the sequence of events when failover happens? 
 
 **ANSWER:**  Route 53 conducts a health check of your application.
  If your application fails 4 consecutive health checks as an example,
   it triggers the next event. Route 53 will disable the resource record 
   for the failed endpoint and no longer serves these records.
    The failover step ensures that traffic gets routed to health endpoints instead of the failed one.
        

HTTPS health checks test whether it’s possible to connect with
the endpoint over SSL and whether the endpoint returns a valid 
HTTP response code. However, they do not validate the SSL certificate 
returned by the endpoint.


**Amazon Route 53 doesnt charge for alias queries to CloudFront distributions, 
Elastic Beanstalk environments, ELB Load Balancers, or Amazon S3 buckets.**

Alias Records are like CNAME records that can map one DNS name www.example.com 
to another. However, Alias records are special in that unlike CNAME records,
you can map an Alias record to a Zone Apex, e.g. company.com, i.e. without
the hostname like ‘www’. You cannot do the same with a CNAME record

To enable DNS Failover for an ELB endpoint, create an Alias record pointing 
to the ELB and set the “Evaluate Target Health” parameter to true.

## Record set

### CNAME vs Alias records 

CNAME used to point foo.example.com to bar.example.com. With same right part of DNS name


An alias record appears as the record type that you 
specified when you created the record, such as A or AAAA. 

CNAME is chargeable, Alias is not.

Aliases differ from a CNAME record in that they are not visible to resolvers. 
Resolvers only see the A record and the resulting IP address of the target record.

### Record Types

* A  : IPv4 
* AAAA : IPv6
* CAA : 
   
   A CAA record lets you specify which certificate authorities (CAs) are allowed to 
   issue certificates for a domain or subdomain.
   (docs ref: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html?shortFooter=true#CAAFormat) 
* CNAME : 

   Specify domain, such ass 'hostname.example.com' 
* MX : 
   
   Used to specify email servers with priorities (e.g. '10 mail.example.com' ) 
* NS :  

   Identifies the name servers for the hosted zone (e.g. 'ns-1.example.com') 
* PTR : the same as CNAME 
* SOA : 

   A start of authority (SOA) record provides information about a domain and 
   the corresponding Amazon Route 53 hosted zone (e.g. ns-2048.awsdns-64.net hostmaster.awsdns.com 1 1 1 1 60) 


## Routing

### Random facts 

Latency based routing. 
   
You can route traff**ic based on the lowest network latency for your end users
so that your end users can experience a faster response time. You would use
 this form of routing when you have resources that serve the same functions 
 located in different availability zones or regions.

