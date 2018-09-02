| AWS Service | Resource/Property | Value |
| ----------- | ----------------- | ------|
| VPC         | Max VPC per region   | 5
| VPC         | Max internet gateways per region | 5  |
| VPC         | Max customer gateways per region | 50 |
| VPC         | Max VPN connections per region | 50 |
| VPC         | Max route tables per region | 200 |
| VPC         | Max elastic IPs per region | 5 |
| VPC         | Max security groups per VPC | 500 |
| VPC         | Max rules per security group | 50 |
| VPC         | Max security groups attached to network interface | 5 | 
| VPC         | Max subnets per VPC | 200 |
| VPC         | Max CIDR blocks per VPC | 5 |
| -------  | ------------------------- | ------ |
| SWF         | Max workflow executions at the same time in domain | 100 000 per domain |
| SWF         | Max workflow execution time | 1 year |
| SWF         | Max number of workflows in domain | 10 000 |
| SWF         | During pooling for a new task, how long SWF will hold TCP connection before new task will be available | 60 seconds |
| SWF         | How many activity tasks you can schedule in one decision | 100 | 
| SWF         | Max workflow history size | 25 000 events | 
| SWF         | Max workflow history retention time | 90 days |
| SWF         | SWF Request size | 1Mb | 
| SQS         | Visibility period for a message (default, min, max)  |  30s,30s, 12h |
| SQS         | Time after which message will be deleted(default, min, max) | 4d,1m,14d | 
| SQS         | Max length of a receipt handle | 1,024 characters |
| SQS         | FIFO Queues: Max messages per second without batching | 300 |
| SQS         | FIFO Queues: Max messages per second with batching | 3000 |
| SQS         | Standart Queues: Max messages per second | unlimited |
| SQS         | Max number of message metadata attributes | 10 |
| SQS         | FIFO Queues: Max inflight messages | 20 000 | 
| SQS         | Standart Queues: Max in-flight messages | 120 000 | 
| SQS         | SQS long polling timeout(default, max,min) | 20,20,1 sec | 
| -------  | ------------------------- | ------ |
| SNS         | Token included in the confirmation message sent to end-points on a subscription request is valid for | 3 days | 
| SNS         | Max topics per account | 100,000 | 
| -------  | ------------------------- | ------ | 
| S3 | Max buckets per account     |   100      |           
| S3 | Bucket name min and max length     |   3, 63         | 
| S3 | TODO | TODO | 
| -------  | ------------------------- | ------ |
| Glacier  | How long expedited retrievals allow you to quickly access data in urgent occasions | 1-5 minutes |
| Glacier  | How many archives can be stored in vault | unlimited |
| Glacier  | How many vaults acn be created per region | 1000 |
| Glacier  | How often Glacier prepares an inventory | every 24h |
| Glacier  | Archive ID length | 138 bytes |
| -------  | ------------------------- | ------ |
| Route53  | Max number of domain names | 50  |
| Route53  | Health check interval (default, min) | 30s, 10s |   |
| Route53  | Max hosted zones | 500|   |
| -------  | ------------------------- | ------ |
| RDS      | Max SQL Server size | 4Tb |
| RDS      | Max number for read replicas | 5 |
| RDS      | Max number for Aurora replicas | 15 |
| RDS      | Max number of RDS DB instances | 40 | 
| RDS      | Backup retention period value(default, min, max) | 1d,1d,35d |
| RDS      | Min and max size of Aurora DB | 10Gb, 64Tb |
| -------  | ------------------------- | ------ |
| IAM      | TODO | TODO | 
| STS      | DurationSeconds parameter which to specify the duration of the role session. Minimum duration:  | 15m |
| -------  | ------------------------- | ------ |
| Lambda   | Lambda execution duration (default, min,max) | 3s,1s,300s | 
| Lambda   | Concurrent executions | 1000 | 
| -------  | ------------------------- | ------ |
| EC2      | Max key-pairs per region | 5000 |
| EC2      | User data max size | 16kb | 
| EC2      | How much cluster placement group offers Ethernet bandwidth connectivity | 10 Gbps | 
| EC2      | How much cluster placement group offer Enthernet bandwidth connectivity via Public IPs | 5 Gbps | 
| EC2      | Max number of EBS volumes that can be attached to EC2i (Linuc, Windows) | 40, 26
| DYNAMO   | Max Query and Scan operation response size | 1Mb | 
| DYNAMO   | Max item size | 400kb |
| DYNAMO   | Max length of partition key | 2048 bytes |
| DYNAMO   | Max length of sort key | 1024 bytes | 
| DYNAMO   | Max number that ListTables action can return | 100 |
| DYNAMO   | Max throughput(reads/writes) | 3000 RCU and 1000 WCU |
| DYNAMO   | Max number of tables per region | 256 |
| DYNAMO   | Table name length restrictions | 3 < tableName < 255 | 
| DYNAMO   | Attribute name length restrictions | 1 < attributeName < 64 | 
| DYNAMO   | Max LSI and GSI per table | 5,5 |
| DYNAMO   | How much items and size BatchGetItem action can retrieve | 100, 16Mb |
| DYNAMO   | How much PutItem/DeleteItem operations and max size, BatchWriteItem can process | 100 PutItem/DeleteItem, 16Mb | 
| DYNAMO   | How long Streams available in logs | 24h |
| CF       | Max number of parameters in template | 60  |
| CF       | Max Stacks per region | 200 |
| CF       | Max Templates per region | unlimited |
| AWS      | Number of port you need to open |what is this about? |
| CloudFront | Number of Point Of Presence, Edge Location, Edge Caches | 134,123,11 | 
| CloudFront | TTL (dafault, min-for-web, min-for-RTMP, max) | 24h, 0, 3600s, 100years | 
| Snowball | Job manifest unlock code length | 25 characters | 
| Snowball | Provided throughput | 10Gbps |
| EC2 Auto Scaling | Launch configurations per region:               | 200  |
| EC2 Auto Scaling | Auto Scaling groups per region:                 | 200  |
| EC2 Auto Scaling | Scaling policies per Auto Scaling group:        | 50   |
| EC2 Auto Scaling | Scheduled actions per Auto Scaling group:       | 125  |
| EC2 Auto Scaling | SNS topics per Auto Scaling group:              | 10   |
| Classic ELB | Connection draining timeout (default, min, max) | 6m,1s,1h | 
            
