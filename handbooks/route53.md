# Route 53
 
## Random facts (remember)

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


## CNAME vs Alias records 

CNAME used to point foo.example.com to bar.example.com. With same right part of DNS name


An alias record appears as the record type that you 
specified when you created the record, such as A or AAAA. 

CNAME is chargeable, Alias is not.

##