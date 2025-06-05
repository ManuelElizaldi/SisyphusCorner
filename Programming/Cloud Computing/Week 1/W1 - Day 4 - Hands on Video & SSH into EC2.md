2025-6-4
# Hands on Video

![[Pasted image 20250604184420.png]]

![[Pasted image 20250604185313.png]]

![[Pasted image 20250604185343.png]]


In source in Networking, you should have a specific list of IPs 

After filling all the fields, you just click Launch Instance. This is way faster than building your own server.

Monitoring the instance:
![[Pasted image 20250604185558.png]]

If you have multiple instances it becomes hard to monitor all of them, so you can use Cloud Watch to monitor all of them

Connecting to the machine:
![[Pasted image 20250604185842.png]]

Opening a new port so people can access the application:
![[Pasted image 20250604190239.png]]

Adding the security group to the instance:
![[Pasted image 20250604190336.png]]

Deleting an instance
![[Pasted image 20250604190501.png]]

Deleted/terminated instances can never be brought back, same for security groups 

#### Question for lesson:
Are security groups rules?

# SSH into a EC2 instance
Standard terminal window can be used to SSH into a EC2 

Once you download the .pem file you can use it to SSH 

The professor reduced the privileges of the .pem file to make it more secure by running the command:

```shell
chmod 400 greatlearning.pem
```

To check the permissions on a file:

```shell
ls -al *.pem
```

It should be read only

To connect you use the following cmd:

![[Pasted image 20250604211531.png]]

Always use sudo apt update inside a EC2 (if you are running ubuntu)

the professor installed apache2 to run a http server 

You can check the inbound rules to determine what ports are open



#### Practice Quiz Question: Which port is required for SSH connection to EC2 instance?
Port 22


