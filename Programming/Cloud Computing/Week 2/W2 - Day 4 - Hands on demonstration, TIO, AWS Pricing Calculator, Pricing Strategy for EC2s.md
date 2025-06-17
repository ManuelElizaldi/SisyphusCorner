# Hands on Demonstration

Simulator app, simu_app.py

You can make an instance 'unhealthy' to test the load balancer algorithm and if the instance does get knocked out 
# TIO



# Pricing Calculator

A solution deployed on the cloud has many AWS features/resources 

How to determine the cost? Project the cost for business analysis. We need to perform this calculation in order to forecast properly. We need a tool to calculate this quickly:

## AWS Pricing Calculator
The calculator lets you add services and configure them to get the estimated total

this is the service selection window:
![[Pasted image 20250612182042.png]]

Pricing depends on region as well, each region has different operating costs. 

OS that you are using in your EC2 comes with a licensing fee 

Inside the service, you can choose the workload:
![[Pasted image 20250612182307.png]]

question -> what if you have a combination of these?

The more CPU and Memory, the more an instance costs 

### Pricing Strategies for EC2 instances usage
*EC2 charges on demand* -> you pay based on how much you use. But AWS offers another options if this does not suit you:
- *Spot* -> like a stock market, if the demand of a EC2 instance goes up, the price goes up and inverse as well. But its still cheaper than the alternatives.
- So you can use them at 3 am to run a batch process and since at 3 am there's no demand, the cost will be low. *important* -> AWS will remove these instances if demand goes up elsewhere. AWS determines when to remove these instances, for example if a *on demand users* needs them
	- Spot instances can, and will, be reclaimed by AWS
	- AZ determines the cost as well for this
	- Good discounts -> up to 90% cheaper
	- Short lived instances

For spot instances will be removed from your environment with a 2 minute warning. 

- *All reserved* -> you reserve a category of an instance for x amount of years, and AWS can give you discounts on your long term commitment.
- *On demand and Reserved* -> a combination of both reserved and on demand. This is useful when you have a part of your application that runs constantly and for a long period of time and another that you prefer on demand
- EC2 Savings Plan & Compute Savings Plan -> You can reserve a family of EC2s or you can reserve the infra (compute, networking, storage)
	- Most flexible plan


EBS (Amazon Elastic Block Storage) -> the storage used by EC2, this is also taken into account for pricing

Data Transfer -> Inbound, outbound and intra-region 
- Inbound -> Data you expect to transfer into your AZ. This is free is free 
- Outbound -> Data you expect to transfer out of your AZ


#### Practice Quiz Question -> AWS pricing is provided at no cost?
True 


## Console-to-Code CLI script
```
aws ec2 run-instances --image-id "ami-020cba7c55df1f615" --instance-type "t2.micro" --key-name "pgpcc-key1" --block-device-mappings '{"DeviceName":"/dev/sda1","Ebs":{"Encrypted":false,"DeleteOnTermination":true,"Iops":3000,"SnapshotId":"snap-0bc1d350c2ac74766","VolumeSize":8,"VolumeType":"gp3","Throughput":125}}' --network-interfaces '{"SubnetId":"subnet-0727dfaf7237b53d0","AssociatePublicIpAddress":true,"DeviceIndex":0,"Groups":["sg-00483a8ccbed52713"]}' --credit-specification '{"CpuCredits":"standard"}' --tag-specifications '{"ResourceType":"instance","Tags":[{"Key":"Name","Value":"httpserver1"}]}' --metadata-options '{"HttpEndpoint":"enabled","HttpPutResponseHopLimit":2,"HttpTokens":"required"}' --private-dns-name-options '{"HostnameType":"ip-name","EnableResourceNameDnsARecord":false,"EnableResourceNameDnsAAAARecord":false}' --count "1" 
aws ec2 run-instances --image-id "ami-020cba7c55df1f615" --instance-type "t2.micro" --key-name "pgpcc-key1" --block-device-mappings '{"DeviceName":"/dev/sda1","Ebs":{"Encrypted":false,"DeleteOnTermination":true,"Iops":3000,"SnapshotId":"snap-0bc1d350c2ac74766","VolumeSize":8,"VolumeType":"gp3","Throughput":125}}' --network-interfaces '{"AssociatePublicIpAddress":true,"DeviceIndex":0,"Groups":["sg-00483a8ccbed52713"]}' --credit-specification '{"CpuCredits":"standard"}' --tag-specifications '{"ResourceType":"instance","Tags":[{"Key":"Name","Value":"httpserver2"}]}' --metadata-options '{"HttpEndpoint":"enabled","HttpPutResponseHopLimit":2,"HttpTokens":"required"}' --private-dns-name-options '{"HostnameType":"ip-name","EnableResourceNameDnsARecord":true,"EnableResourceNameDnsAAAARecord":false}' --count "1" 
aws elbv2 create-target-group --name "c2c-tg" --target-type "instance" --health-check-path "/health.html" --healthy-threshold-count "2" --unhealthy-threshold-count "2" --health-check-timeout-seconds "5" --health-check-interval-seconds "30" --matcher '{"HttpCode":"200"}' --port "80" --protocol "HTTP" --protocol-version "HTTP1" --ip-address-type "ipv4" --health-check-port "traffic-port" --health-check-protocol "HTTP" --vpc-id "vpc-08260fadfe618161a" 
aws elbv2 register-targets --target-group-arn "arn:aws:elasticloadbalancing:us-east-1:715923492212:targetgroup/c2c-tg/4edc3cf59af87477" --targets '{"Port":80,"Id":"i-018ae527852eae03b"}' '{"Port":80,"Id":"i-0546c38dae3444d14"}' 
aws elbv2 create-load-balancer --name "c2c-lb" --subnets 'null' --subnet-mappings '{"SubnetId":"subnet-0727dfaf7237b53d0","AllocationId":null,"IPv6Address":null,"PrivateIPv4Address":null,"StaticIp":null}' '{"SubnetId":"subnet-0691aeeaeacbafe0d","AllocationId":null,"IPv6Address":null,"PrivateIPv4Address":null,"StaticIp":null}' '{"SubnetId":"subnet-0592d5eac25957d3a","AllocationId":null,"IPv6Address":null,"PrivateIPv4Address":null,"StaticIp":null}' '{"SubnetId":"subnet-0dae716df85d5a475","AllocationId":null,"IPv6Address":null,"PrivateIPv4Address":null,"StaticIp":null}' '{"SubnetId":"subnet-093a6b02aef8c5845","AllocationId":null,"IPv6Address":null,"PrivateIPv4Address":null,"StaticIp":null}' '{"SubnetId":"subnet-0fbe2ee8b235e70db","AllocationId":null,"IPv6Address":null,"PrivateIPv4Address":null,"StaticIp":null}' --security-groups "sg-00483a8ccbed52713" "sg-0dd6cbde681676fea" --scheme "internet-facing" --type "application" --ip-address-type "ipv4" 
aws elbv2 create-listener --protocol "HTTP" --port "80" --ssl-policy 'null' --default-actions '{"Type":"forward","TargetGroupArn":"arn:aws:elasticloadbalancing:us-east-1:715923492212:targetgroup/c2c-tg/4edc3cf59af87477"}' --load-balancer-arn "arn:aws:elasticloadbalancing:us-east-1:715923492212:loadbalancer/app/c2c-lb/d2698cecbfc08a14" 
```