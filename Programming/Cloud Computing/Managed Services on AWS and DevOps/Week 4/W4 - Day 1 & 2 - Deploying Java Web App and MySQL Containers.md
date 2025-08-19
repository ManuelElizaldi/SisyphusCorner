[[MySQL]] [[Containers]] [[Java]]

Bundling mechanisms - these depend on the programming language that you are using 

Tom Cat - Environment that runs Java 

## Image Downloading
Docker Command: `docker pull tomcat:jre8` - jre8 is the version we are interested in.
- This command downloads the layers needed for this image

## Tagging port from EC2 to Container - Port Mapping
-p host:container 

example: `-p 80:8080`

The requests called to 80 will be forwarded to 8080

## Running a web app from a container 
The run command:
`docker run -d -p 80:8080 tomcat:jr8` -> gives you the id 
80 -> host 
8080 -> container 

After entering the command, you will have a web app running from your container

`docker ps -a` -> it should show the container 

`ps -ef | grep [d]ocker` -> shows the running processes 


## Running and Stopping
`docker stop containerName` - after running this, your web app wont load (obviously) because there is no host

The advantage of using containers is that if demand goes up, you can start them up very fast and if demand goes down, you can stop them - containers are very elastic

Another way of stopping a docker process: `sudo kill -9 processID` 
- This is a harsher way of stopping a process, the professor did not recommend it 

## Connecting a container to a volume 
Downloading a file must land in the container - you need a pipe between the volume and the container 

`docker run -v <host_path>:<container_path> <image_name>`

You can access files in the container from host and the container can access files from the host. *two sided channel*
### Command flags
-d -> detach
-p -> port tag 
-v -> port mount

![[Pasted image 20250818190421.png]]
#### Multiple containers can be created from the same image

Containers, even though they are ephemeral, they can have data that lives beyond their life cycle. 

## Getting into a container
`exec -it container_name bash`

## Store the work inside a container - Commit as image 

