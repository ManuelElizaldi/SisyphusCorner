**Which approach allows the capacity to closely lead the utilization for enterprise applicatons?**
Containers

**The primary difference between virtual machines and containers is that virtual machines contain a full operating system, whereas containers share the host operating system's kernel and only contain the minimal operating system components needed to run the application.**
True

**Which of the following best illustrates the relationship between an image and a container?**
Executable and process
a container is a _running instance_ created from an image, just like a process is an executing instance of an executable file. The image is the static template (executable), the container is the live runtime (process). - i think

**Assume a container based deployment. Where should the persistent client data be stored?**
Data Storage outside the container
Storing long-term client data in the container filesystem is generally not recommended for several reasons:

- Ephemerality of Containers: Containers are designed to be ephemeral and stateless. They can be stopped, started, or replaced at any time, and when this happens, any data stored in the container's filesystem can be lost. This makes it unreliable for long-term storage of client data.
- Backup and Recovery: Implementing backup and recovery strategies is more challenging when data is stored on container filesystems. Containers can be distributed across different hosts and environments, making it difficult to create cohesive backup policies.
- Portability and Migration: Containerized applications are often moved between different environments (development, testing, production). Having client data inside the container can complicate these migrations, as the data would need to be moved along with the containerized applications.
- Performance: Storing data in container filesystems can degrade performance, especially under high loads or with large datasets. Dedicated storage solutions often have optimizations for performance and reliability that are not available in container filesystems.

There are more suitable alternatives for persistent storage, such as network-attached storage (EFS), databases, object storage services (S3), or other managed storage solutions that can be mounted to containers. These options are designed to persist data beyond the lifecycle of individual containers and offer better scalability, redundancy, and backup options.

For these reasons, it's generally better to keep containers stateless and use external storage solutions for persisting client data. This way, the application architecture remains flexible, reliable, and scalable.