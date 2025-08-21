[[ECS]]
# AWS ECS
Containers are horizontally scaled 

Managed Kubernetes - you give me the container and I can manage everything else

## How it works
Load Balancer is needed + its target group -> inside the target group you have EC2 instances. 

AWS ECS can also create the set up (load balancer + target group)

AWS can access a Private Ducker Repository 
- You create the image from a host PC and push it to the private repo. The host PC needs docker 

You also need to specify the ASG (auto scaling group) -> if CPU > 80% + if CPU < 80% - -> but what capacity is it adding?
- *Added capacity = Task (pod)* -> group of containers. 
	- For example, a pod contains 2 containers (derived from their respective images) they both live and die together.  

So, the ASG is adding tasks/pods

> [!NOTE] Task vs Pod
> Task is refereed to a group of containers in AWS. In Kubernetes this is referred to as a Pod. 

## How many tasks per EC2?
more tasks = larger machine = reduced elasticity - vertical or horizontal scaling? 
- *There is no right or wrong, depends on the application.* 

*If you adopt a horizontal scaling strategy*, then the EC2 instances need to be as small as possible (reduced cost benefit as well) and provide small tasks on each EC2. 
- Try to have a 1 to 1 mapping - 1 EC2 1 task - this is per AWS best practices. If you can do this, then go for 1 to many relationship but this will make the system a bit less resilient 
![[Pasted image 20250820190240.png]]


## Fargate
The new release of ECS - you can specify everything and it will manage it on your behalf 

This managed service can help you set all the above easier 

Fargate allows for code to infrastructure 


# ECS TIO

The goal The following are the goals of this hands-on:
1. Launch an EC2 instance 
2. Build the Apache Tomcat image 
3. Create a private repository in ECR and push the image to the registry 
4. Create a cluster, a task definition and service in ECS with auto scaling 
5. Access the application via web browser

---

## Launching an Ec2
We launch an instance

Inside the instance dashboard, we select the instance we just created and then go to Actions -> Security -> Modify an IAM role and select `LabInstanceProfile`.

## Working with images and containers 
I connected into the ec2 instance (same as usual - ssh) and run the following commands:
```
wget https://d6opu47qoi4ee.cloudfront.net/dockerinstallscript.sh bash 
dockerinstallscript.sh
exit
```

refresh then

`docker version` just to confirm the installation

now we run the following commands:

```
sudo chown ubuntu:ubuntu -R /opt 
cd /opt 
docker images 
docker run --rm busybox:latest /bin/echo "Hello world" 
wget https://d6opu47qoi4ee.cloudfront.net/project-container/Dockerfile 
docker build -t helloworld . 
docker run -d -p 80:8080 helloworld 
docker ps -a
```

1. changes the owner of the folder
2. changes directory 
3. checks for images - nothing comes up because we don't have anything installed yet 
4. runs the image with the --rm command, meaning it removes it once its done, since we are adding the /bin/echo we are telling this container to print "Hello World"
5. downloads Dockerfile
6. builds the image with the -t tag flag as "helloworld" and the . tells docker to use the current directory 
7. runs the image that was downloaded in detach mode (-d) and tagging the port 80 to 8080 
8. checks for running processes 

If you open the public IP of the EC2 instance you see a tomcat website 


## Creating a private repository on ECR - Elastic Container Registry to push image we built
*Amazon Elastic Container Registry (ECR) is a fully managed container registry that makes it easy to store, manage, share, and deploy your container images and artifacts anywhere.*

Open the ECR console and created a repository 
![[Pasted image 20250820194701.png]]

You can determine if its mutable

After creating the repository I connected back into the instance and ran the commands:

```
sudo su
apt install awscli -y
aws configure
```

This installs the aws cli tools and opens them
After running `aws configure` I created these settings:
![[Pasted image 20250820195143.png]]

Inside the ECS console I selected the repository we created and then clicked on 'View Push Commands'. There was this command: `aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 715923492212.dkr.ecr.us-east-1.amazonaws.com`

the above command give you the credentials as a json to push to the repo

then I ran `docker tag helloworld:latest 715923492212.dkr.ecr.us-east-1.amazonaws.com/helloworld:latest` - this tags the image

finally we push with: `docker push 715923492212.dkr.ecr.us-east-1.amazonaws.com/helloworld:latest`

After all those commands, inside the repo we created we have this:
![[Pasted image 20250820195906.png]]

## Creating a cluster inside ECS - Elastic Container Service
*Amazon Elastic Container Service (Amazon ECS) is a highly scalable and fast container management service that makes it easy to run, stop, and manage containers on a cluster.*

We create a cluster - we only define the name 

you can determine the infrastrucutre:
![[Pasted image 20250820200404.png]]

### Then we create a task (pod)
we put the URI `715923492212.dkr.ecr.us-east-1.amazonaws.com/helloworld:latest` created in the ECR inside the Container -1 section of the tasks creation like so:
![[Pasted image 20250820200947.png]]

The container port is 8080, everything else was left defautl

### Creating service inside ECS Cluster
Then inside the ECS Cluster we created we go to the service tab and create a service

Under the task definition family drop down we select the ECSTASK we created 

Inside this creation window is where we define how many tasks we want 

We create a new security group under networking and open port 80 and 8080 from anywhere 

We opened a load balancer and target group

We also defined the Service auto scaling - 1 minimum task 4 maximum. We selected CPU usage as a metric for scaling and 70 as target value (not sure what this is doing)

After this we click on create

*Creating process*
![[Pasted image 20250820202154.png]]


Inside the EC2 management console we can see that both tasks are healthy:
![[Pasted image 20250820202335.png]]

If we open the DNS `ecslb-1420632327.us-east-1.elb.amazonaws.com` from the load balancer the tomcat instance will open on the web browser!


--- 
### Reference
[ECS TIO](https://d6opu47qoi4ee.cloudfront.net/labs/tio/containers/ecs_tio.pdf)