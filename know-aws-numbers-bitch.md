| AWS Service | Resource/Property | Value |
| ----------- | ----------------- | ------|
| VPC         | Max VPC per region   | 5
| VPC         |   Max internet gateways per region        |     5     |
| VPC         | Max customer gateways per region | 50 |
| VPC         | 50 VPN connections per region | 50 |
| VPC         | Max route tables per region | 200 |
| VPC         | Max elastic IPs per region | 5 |
| VPC         | Max security groups per VPC | 500 |
| VPC         | Max 50 rules per security group | 50 |
| VPC         | Max security groups attached to network interface | 5 | 
| VPC         | Max subnets per VPC | 200 |
| VPC         | Max CIDR blocks per VPC | 5 |
| ----  | ---- | ---- |
| SWF         | Max workflow executions | 100 000 per domain |
| SWF         | Max workflow execution time | 1 year |
| SWF         | Max number of workflows in domain | 10 000 |
| SWF         | During pooling for a new task, how long SWF will hold TCP connection before new task will be available | 60 seconds |
| SWF         | How many activity tasks you can schedule in one decision | 100 | 
| SWF         | Max workflow history size | 25 000 events | 
| SWF         | Max workflow history retention time | 90 days |
| SWF         | SWF Request size | 1Mb | 
| SQS         | Visibility period for a message (default, min, max)  |  30s,30s, 12h |
| SQS         | Time after which message will be deleted(default, min, max) | 4d,1m,14d | 
| SQS         | FIFO Queues: Max messages per second without batching | 300 |
| SQS         | FIFO Queues: Max messages per second with batching | 3000 |
| SQS         | Standart Queues: Max messages per second | unlimited |
| SQS         | Max number of message metadata attributes | 10 |
| SQS         | FIFO Queues: Max inflight messages | 20 000 | 
| SQS         | Standart Queues: Max inflight messages | 120 000 | 
| ----  | ---- | ---- |
| SNS         | Token included in the confirmation message sent to end-points on a subscription request is valid for | 3 days | 
| ----  | ---- | ---- | 
|
