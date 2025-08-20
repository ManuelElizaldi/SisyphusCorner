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
Before you commit, you need to stop the process. If it's running, its not in a consistent state

`docker commit -"author" -m"message" container_name name_of_your_image`

All the work that has been done can be saved as an image by running the command above

## Run a Microsoft native (c++ or .net) application on linux
This is possible if you inject the application into a container and run it from linux 

## MySQL 
`docker pull mysql`

Any database when opened for the first time asks you for the password to be able to perform admin tasks. There is a feature to tell docker the database password: 
`docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password image_name(mysql)`

Going inside the container that is running mysql:
`docker exec -it container_name bash`

if you do `ps -ef` inside a mysql container, nothing will happen, some of this commands are suppressed by the layers for safety. Same happens with `kill -9 l`

`mysql -u root -p` then you enter password
 
 
 
 ## Saving image on a USB 
`docker save image_id > tomcatapp.tar` This will create the assembly/config file that can create the image

`docker laod < config_file.tar` loading the image from an external source

