# Elastic beanstalk (EB)

## Random facts

Configuration means highly available if: 

**Edit your environment configuration settings, select 2 or more
 instances for Auto Scaling minimum, and set Multiple Availability Zones to “Any 2”.**
 
 Elastic Beanstalk manages the Amazon SQS queue and runs a daemon process 
 on each instance that reads from the queue. When the daemon pulls an item 
 from the queue, it sends an HTTP POST request locally to
  http://localhost/ with the contents of the queue message in the body.
  
## Host manager (TODO other info)
The host manager is responsible for:

* Deploying the application
* Aggregating events and metrics for retrieval via the console, the API, or the command line
* Generating instance-level events
* Monitoring the application log files for critical errors
* Monitoring the application server
* Patching instance components
* Rotating your application’s log files and publishing them to Amazon S3