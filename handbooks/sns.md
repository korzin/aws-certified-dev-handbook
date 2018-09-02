
# SNS

## Random facts (remember)

Token included in the confirmation message sent to end-points on a subscription 
request is valid for 3 days.

Amazon SNS does not currently support forwarding messages to Amazon SQS FIFO queues. 
You can use SNS to forward messages to standard queues.

The “fanout” scenario is when an Amazon SNS message is sent to a topic and 
then replicated and pushed to multiple Amazon SQS queues, HTTP endpoints, 
or email addresses. This allows for parallel asynchronous processing

Amazon SNS guarantees that each message is delivered to Amazon SQS at least once


Avalable endpoins include: HTTP, HTTPS, Email, Email-JSON, SQS, Webapp, mobile app, LAMBDA, SMS

SNS endpoint API: CreatePlatformEndPoint

## API 

AddPermission
ConfirmSubscription
CreatePlatformApplication
CreatePlatformEndpoint
CreateTopic
DeleteEndpoint
DeletePlatformApplication
DeleteTopic
GetEndpointAttributes
GetPlatformApplicationAttributes
GetSubscriptionAttributes
GetTopicAttributes
ListSubscriptions
ListSubscriptionsByTopic
ListTopics
Publish
RemovePermission
SetEndpointAttributes
SetSMSAttributes
SetSubscriptionAttributes
SetTopicAttributes
Subscribe
Unsubscribe