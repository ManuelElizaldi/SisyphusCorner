[[Data Streaming]] [[AWS Kinesis]] [[AWS]] [[Cloud]]
# Kinesis Data Steam
Fully managed platform to collect, process and analyze real time streaming data. 

Kinesis allows you to process data as it arrives allowing real time analytics, instant fraud detection and live dashboards. 

Ordered sequence of data records 
## Components
Data Record -> The unit of data stored by kinesis stream 

Data Stream -> Represents a group of data records. The data records in a data stream are distributed into shards. 

Retention Period -> Length of time data records are accessible from stream. A kinesis data stream stores records from 24 hours by default, up to 365 days. 

Kinesis Client Library -> Ensures that for every shard there is a record processor running and processing the shard. 

Producer -> puts data records into shards 

Consumer -> gets data records from shards

Shard -> It has a sequence of data records in a stream 


![[Pasted image 20260330190433.png]]


# Case Study 
An EC2 instance is producing logs, these will be pushed/captured by Kinesis Data Streams. From Kinesis Data streams it gets consumed by Amazon Kinesis Data Firehose. The data from Firehose then gets stored in S3.

# Lab
Created a EC2 instance. 

We ssh into instance, then change to root user and update the system. 

We install the LAMP and HTTPD server
`sudo dnf install -y httpd mariadb105 php php-mysqlnd`
- httpd -> http daemon. Basically this is an apache web server. 

We start the httpd server and enable
`sudo systemctl start httpd` + `sudo systemctl enable httpd`

we navigate to the HTML folder path
`cd /var/www/html`

Downloading a sample/testing html website:
`curl -O -L -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36" "https://labresources.whizlabs.com/094ba567ebb44c80c99f06f70ba6b44a/marvel-master.zip"`

after this we use http://ip/marvel-master to enter to the website we are hosting

changing to the directory cd `/var/log/httpd/` 
## Storing the continuous logs 
What are httpd groups? What is the purpose of this with kinesis and kinesis firehose
- Groups are needed by default, the logs at `/var/log/httpd/` belong only to the root user, and ONLY the root user. Permissions for this folder only let the root user interact with it. The Kinesis agent runs as ec2-user, not root. So without permission changes the ec2 user wont be able to access the logs. This explains the following steps:
- least privilege through group membership <- This is why we create groups in linux 

First we need to add the httpd group to the EC2 instance using the command:
`groupadd httpd`

then we add the ec2-user to the httpd group
`usermod -a  -G httpd ec2-user`

we can check the httpd groups with:
`groups`

We also need to change the ownership of the httpd folder to the httpd group:
`sudo chown -R root:httpd /var/log/httpd`

We are also changing the directory permissions of /var/log/httpd and its sub directories to add group write permissions 
`sudo chmod 2775 /var/log/httpd`
`find /var/log/httpd -type d -exec sudo chmod 2775 {} +`

## Creating Kinesis Data Stream
Create a data stream, name it and left every setting on default.
- On-demand data stream capacity. This is for when you don't know the demand patters. 

Once created we go to the data stream configuration -> encryption and we enable server side encryption with default encryption key. 

## Creating a Bucket
This bucket will store all of the data from the Kinesis Firehose


## Creating AWS Data Firehose - Kinesis Data Firehose 
Once the streaming service gets the data from the logs, then we need to push the data somewhere. It is not possible to post the data from the Kinesis Data Streams. So we will use Kinesis Data Firehose.
- Why is it not possible to post the data from the kinesis data streams? *Answer on the bottom of notes.*
	

Inside Kinesis Data we select the Firehose service. Then we create a Firehose. 
- We select the source -> Amazon Kinesis Data Stream 
- Destination - S3

Then we name it

Then in source settings, we select the *Data Stream* we created earlier

We also select the bucket we created 

**Buffer Interval** -> This determines the time to collect data. The bigger the buffer, the more time there is to collect data. the lower the interval sends data more frequently - good for shorter cycles of data activity. 
- Real cases for this? 

In Advanced settings -> We only chose the Existing IAM role Kinesis Fire hose policy 
- What does it need? 

## Configuring Kinesis Agent 
First we need to install the Kinesis agent on our EC2
`sudo dnf install -y https://s3.amazonaws.com/streaming-data-agent/aws-kinesis-agent-latest.amzn2.noarch.rpm`

we edit the kinesis agent json config:
`sudo nano /etc/aws-kinesis/agent.json`

we removed what was in there, and pasted this:
```json
{

    "cloudwatch.emitMetrics": true,

    "kinesis.endpoint": "",

    "firehose.endpoint": "",

    "awsAccessKeyId": "A*****************",

    "awsSecretAccessKey": "B******************",

    "flows": [

      {

        "filePattern": "/var/log/httpd/access_log",

        "kinesisStream": "whiz-data-stream",

        "partitionKeyOption": "RANDOM"

      }

    ]

}
```


then we restart the service:
`sudo service aws-kinesis-agent stop`
`sudo service aws-kinesis-agent start`

Then we check the log at: `cd /var/log/aws-kinesis-agent/`

You can check if the service started properly by going through the log:
`tail aws-kinesis-agent.log | grep "completed"`

![[Pasted image 20260331200410.png]]

**ASK CLAUDE** -> What is the Kinesis Agent


## Testing the real-time streaming of data 
Let us test by hosting the above sample website on multiple browsers or do some click activity on the website. The related logs will be collected on the listed S3 bucket.

I opened several of the same page on my browser and clicked around. 

An example of a stream created:
![[Pasted image 20260331201037.png]]

### Checking CloudWatch metrics of Kinesis Data stream and Firehose
Inside Kinesis -> data stream we created -> monitoring tab
- Here we can monitor different metrics regarding the data stream process. 
	- There's a counter for GET records

Inside Firehose we can also view a similar monitoring window:
![[Pasted image 20260331201632.png]]


> [!NOTE] **Do you know ?**
> Amazon Kinesis Data Streams supports the concept of shards, which are the fundamental units of data capacity within a stream. Each shard in a Kinesis Data Stream can handle up to 1 MB/sec of data input and 2 MB/sec of data output. However, with the use of Kinesis Data Firehose, you can easily ingest data into Kinesis Data Streams at a much higher rate, exceeding the individual shard limits.

# Take Away
Browser request hits your EC2 web server (httpd/Apache)
      ↓
httpd writes the request to /var/log/httpd/access_log
      ↓
Kinesis Agent (watching that file continuously)
detects new line → packages it → sends to Data Stream
      ↓
Kinesis Data Stream holds the record in a shard
(multiple consumers could read from here)
      ↓
Kinesis Firehose (one of those consumers)
buffers records for 60 seconds → writes batch to S3
      ↓
S3 bucket stores the log files
      ↓
(Could then use Athena + QuickSight to analyze!)

# Why is it not possible to post the data from the kinesis data streams?
Kinesis data streams is designed for one thing -> **real-time streaming**.

Kinesis data streams stores data in shards temporarily. It lets consumers read the data in real time. But it does not have ability to write or deliver data by itself.

Someone needs to pick up the stream

- Kinesis Data Stream -> conveyor belt
- Kinesis firehose -> the worker who picks up the item and sends it to S3 

Kinesis Data Streams is built for **real-time processing** — multiple consumers can read from it simultaneously. 