AWS Lambda
-----------


Lambda allows you to upload code and dependencies for function
 packages: 
 1) From a zip file in AWS S3  
 2)  Uploaded directly from elsewhere


When referencing the remaining time left for a 
Lambda function to run within the function's code 
you should use context object

 **A Lambda deployment package contains: Function code and libraries
  not included within the runtime**   
  
**Lambda requires you to specifically allocate certain resources. The following can you adjust directly: 1) Execution timeout 2) Memory**
  
## Lambda supported languages 
* Node.js
* Python 
* Java 
* C#
* Go
    
## Lambda event sources 
* HTTP requests through API Gateway
* CloudWatch scheduled events
* S3 file uploads
* SNS
* SQS (Poll-based)
* EC2 instance start
* Amazon API Gateway
* DynamoDB stream changes
* Direct invocations
* etc.  
  
## Lambda pricing

Lambda is priced based on number of requests and Duration 
of code execution considering memory that is allocated to the function.


