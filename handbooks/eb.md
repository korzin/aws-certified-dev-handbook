# Elastic beanstalk (EB)

Configuration means highly available if: **Edit your environment configuration settings, select 2 or more
 instances for Auto Scaling minimum, and set Multiple Availability Zones to “Any 2”.**
 
 Elastic Beanstalk manages the Amazon SQS queue and runs a daemon process 
 on each instance that reads from the queue. When the daemon pulls an item 
 from the queue, it sends an HTTP POST request locally to
  http://localhost/ with the contents of the queue message in the body.

**Environment URL** :

     myapp.us-west-2.elasticbeanstalk.com

## Supported platforms 

* Docker
* Go
* Java SE and with Tomcat
* .NET on Windows Server with IIS
* Node.js
* PHP
* Python
* Ruby

## Resources that EB can create
* Main components
    * EC2
    * ELB
    * SG
    * AutoScaling
    * SQS
    * Additional EC2 for batching process for SQS
    * Other
* Persistence 
    * S3    
    * EFS 
    * EBS Elastic Block Store 
    * DynamoDB 
    * RDS

## Host manager (TODO other info)
The host manager is responsible for:

* Deploying the application
* Aggregating events and metrics for retrieval via the console, the API, or the command line
* Generating instance-level events
* Monitoring the application log files for critical errors
* Monitoring the application server
* Patching instance components
* Rotating your application’s log files and publishing them to Amazon S3