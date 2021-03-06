# SQS

## Message metadata

Supported types include String, Number, and Binary. 

## URL

     https://sqs.us-east-2.amazonaws.com/123456789012/MyQueue


## Limits 

The default (minimum) visibility timeout for a message is 30 seconds. The maximum is 12 hours.

If you need to implement priority in Q, the you better two create two different Q;

Messages can be stored in the queue `1 minute < t <  to 14 days` . The time is customizable. 
The default setting is `4 days`. `Once message limit is met, messages are automatically deleted.`


## Brief description and benefits

* Security 
 
  You control who can send messages to and receive messages
   from an Amazon SQS queue. Server-side encryption (SSE) lets you transmit 
   sensitive data by protecting the contents of messages in queues using keys 
   managed in AWS Key Management Service (AWS KMS).

* Durability 
    
  To ensure the safety of your messages, Amazon SQS stores them on multiple 
  servers. Standard queues support at-least-once message delivery, and FIFO
   queues support exactly-once message processing.

* Availability 

  Amazon SQS uses redundant infrastructure to provide highly-concurrent 
  access to messages and high availability for producing and consuming messages.

* Scalability

  Amazon SQS can process each buffered request independently, scaling 
  transparently to handle any load increases or spikes without any provisioning
   instructions.

* Reliability
   
   Amazon SQS locks your messages during processing, so that multiple producers
    can send and multiple consumers can receive messages at the same time.

* Customization
  
   Your queues don't have to be exactly alike—for example, you can set a default
    delay on a queue. You can store the contents of messages larger than 256 KB
     using Amazon Simple Storage Service (Amazon S3) or Amazon DynamoDB, 
     with Amazon SQS holding a pointer to the Amazon S3 object, or you can split
      a large message into smaller messages.

## Architecture



## API 

SetQueueAttributes  to set attributes
GetQueueAttributes  to get attributes 

ChangeMessageVisibility change msg visibility