Consider an application is binding to port 3000 in a container, however, the host virtual machine has a firewall rule to allow bidirectional traffic on 80. How can the container serve this traffic?
Using the flag -p

Which of the following is the correct hierarchy for ECS components?
Assume "<" denotes “lives inside”.
Container<Task<Service<Cluster|

ECS fargate requires cloud administrators to manage the EC2 instances including operating system security patches.
False
AWS Fargate is a technology that you can use with Amazon ECS to run containers without having to manage servers or clusters of Amazon EC2 instances. With AWS Fargate, you no longer have to provision, configure, or scale clusters of virtual machines to run containers. This removes the need to choose server types, decide when to scale your clusters, or optimize cluster packing.

Which of the following Docker command can be used to download an image?
Pull
Docker pull will download an image from either DockerHub or a private repository and store it on the host VM.

What is the maximum amount of RAM a container can consume if the memory flag is not used?
As much as the host instance has free
As per Docker documentation:
-m, --memory="" Memory limit (format: <number>[<unit>]). Number is a positive integer. Unit can be one of b, k, m, or g. Minimum is 4M.

Creating a custom image out of a modified container can be analogous to __
Committing a change in a Git repository
Docker commit and Git commit seem to have the same principle - take the updated details and commit to a repository.

The docker command used to log into a shell in a running container is _
exec
The `docker exec` command runs a new command in a running container. Using it with -it and bash gives us a terminal shell to a container running in detached mode.

How long does a container stay in the running state if it is not manually halted?
As long as the container’s PID 1 is running
Container’s PID 1 is the application process that keeps the container alive. As soon as PID 1 finishes its task and exits, the container also goes into the exited state and is removed if the --rm was used to create it.


