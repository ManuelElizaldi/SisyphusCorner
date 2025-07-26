
# Simple Queue Service
Pull based model - you define queues

## Characteristics
Pull based service -> The application has to iterate and wait to receive data.

SQS holds data and then sends it 

**Producer** - application, SNS, many services can be producers and **consumers** of these messages

Messages have a *finite* lifetime, SQS does not hold data forever. 

The SQS has a URL 

SQS once created can be configured 

### Permissions
Who can deposit messages in the queue 

Principal -> user, role or account that is allowed to access the SQS queue 

## Types of Queues
- FIFO -> first in first out 
- Standard -> Faster performance in middleware communicating 
	- There might be duplicate message - for this you need to consider using a deduplication method - architectural design considerations

**Order vs Speed**

*Limited data Storage* -> There's a limit to size of queues, if the payload is too big you can store it in a S3 or database and then the queue will carry a message indicating the location of the payload. 
- if you do have a message that exceeds the limit and you don't want to use S3 you need to split it into multiple messages or use a database to store the message. 


> [!NOTE] SQS Prefers small messages
> SQS is built for smaller messages


## SQS Pipeline

Produces -> SQS Content -> consumer:
							- There are consumer libraries that can be used to communicate with SQS to check if there's something 
							- EC2
							- ASG -> TG -> group of instances - This allows to scale instances depending on the number of messages
							

![[Pasted image 20250722222143.png]]

ASG are not only web related, there are other use cases for them. 

Content can be a file, in voices, pdfs, etc. 

### Re-drive - Deadletter Queue - Failure Pipeline

![[Pasted image 20250722222551.png]]

Example -> You are receiving files from a customer that need to be in a specific format, if something gets messed up in the format and there's an error, the SQS system will forward this 'message/file' to the deadletter queue to be handled by it. 

you can combine SQS with SNS to send a message to the client to let them know there was an error with their file
![[Pasted image 20250723170435.png]]

Setting up the **Redrive** is the same as setting up the regular pipeline, except that you might want to hold the messages for longer. There is no feature to create a deadletter queue, you take a regular one and set it up as a redrive/deadletter
![[Pasted image 20250723173033.png]]


### Advantage - Elasticity rules are different from the SQS pipeline & deadletter

## SQS Pricing Model
Pay only for what you use

FIFO -> More expensive - but guarantees message order
Standard -> less expensive

Each 64 KB chunk of a payload is billed as 1 request 
- 256 KB are billed as 4 requests 

Every Amazon SQS action counts as a request

## Reliability 
Stores all queues in a single highly availability zone with redundant AZ. High availability

### Fan Out - Use cases - E commerce
Once an order is placed, several queues start up:

Order - a message is sent to whomever is in charge of packing the new order

notifications to user - your order has been confirmed and you could also buy x,y,z

warehouse - maybe inventory needs to be updated

All of these processes can start up based on a message received by the queue. This can be programmed without a single line of code 


## SQS + SNS
You subscribe to the SQS through the SNS so that you can listen/pull messages. You indicate the end point ARN in the SNS. After that you have subscribed and you can push messages to SQS.
![[Pasted image 20250723173917.png]]

SNS send message -> SQS picks it up -> you pull for it

## SQS + S3 + SNS
Create a bucket -> properties -> event -> notification 

The S3 needs permissions from the SNS 

*The pipeline looks like this*:
document is dropped into S3 -> triggers event -> message is sent to SNS -> SNS sends a notification to SQS -> There is a new message in SQS -> sends out email


--- 

# SNS & SQS TIO - Notes

Create SNS -> Create SQS (updated permissions with json) -> SNS subscribes to SQS 

Inside SNS:
![[Pasted image 20250724180325.png]]


Json used in SQS to grant our account permission to pull

```json
{
 "Version": "2008-10-17",
 "Id": "__default_policy_ID",
 "Statement": [
 {
 "Sid": "__owner_statement",
 "Effect": "Allow",
 "Principal": {
 "AWS": "715923492212"
 },
 "Action": [
 "SQS:*"
 ],
 "Resource": "arn:aws:sqs:us-east-1:715923492212:content_q"
},
{
 "Sid": "Allow-SNS-SendMessage",
 "Effect": "Allow",
 "Principal": {
 "Service": "sns.amazonaws.com"
 },
 "Action": ["sqs:SendMessage"],
 "Resource": "arn:aws:sqs:us-east-1:715923492212:content_q",
 "Condition": {
 "ArnEquals": {
 "aws:SourceArn": "arn:aws:sns:us-east-1:715923492212:content_topic"
 }
 }
}
 ]
}

```

From SNS -> publish message. The message has different attributes. I am assuming each end point has different attributes as well. Right now the end point is SQS, these are the current attributes that we can select:
![[Pasted image 20250724180608.png]]

After publishing messages I opened SQS and polled for messages:
![[Pasted image 20250724180817.png]]

