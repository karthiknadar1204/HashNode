---
title: "Docker for Beginners: Getting Started with Containerization"
datePublished: Mon Jun 05 2023 18:15:09 GMT+0000 (Coordinated Universal Time)
cuid: clij69ki600010ajqf7cg9pta
slug: docker-for-beginners-getting-started-with-containerization
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685987422687/cffd17a0-2e0d-47f2-a0eb-a0a8ed48109d.webp
tags: docker, devops, containerization, docker-images, containerization-vs-virtualization

---

In this blog, we will dive into the world of Docker and explore its basics, shedding light on its fundamental concepts, advantages, and use cases. Whether you are a developer, system administrator, or IT professional, this beginner's guide aims to equip you with the knowledge needed to harness the power of containerization and leverage Docker for your software development and deployment needs.

## What is docker?

Docker is an open-source platform that enables developers to automate the deployment, scaling, and management of applications using containerization. It provides a way to package software and its dependencies into standardized units called containers.

## What is a docker image?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987522414/bc02598f-b16c-429b-b929-54a1c9ab76ff.jpeg align="center")

A Docker image is like a ready-to-use package that includes all the necessary components for running an application. It contains the application's code, dependencies, libraries, and tools. Think of it as a blueprint or template that can be used to create running instances called Docker containers.

## What are docker containers?

**Docker Containers are the ready applications created from Docker Images.** A container is a lightweight and isolated runtime environment that packages an application and its dependencies together. It provides a consistent and predictable environment for running the application, regardless of the underlying infrastructure.

Containers are based on the concept of containerization, which allows applications to be encapsulated with their required dependencies, libraries, and configurations, ensuring that they run reliably and consistently across different computing environments.

In simpler terms, a container can be thought of as a standalone and portable unit that contains an application and everything it needs to run, making it easy to deploy and manage applications in a standardized manner.

## Are dockers and containers the same?

Docker uses containerization technology to create and manage containers. It leverages the concept of containers and provides an interface to build, manage, and deploy them efficiently. Docker uses container images, which are blueprints or templates that define the contents and configuration of a container. Docker images are used to create and run containers.

A container is a lightweight and isolated runtime environment that packages an application along with its dependencies, libraries, and configurations. It provides a consistent and portable environment for running applications, ensuring that they work consistently across different systems and environments.

So, while Docker is the platform that enables containerization and provides the tools to manage containers, a container is the runtime instance of an application that runs in an isolated and self-contained manner. Docker and containers work together to provide an efficient and scalable way to package, deploy, and manage applications.

## What is containerization?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987698459/ca849f88-9002-48ee-8ec3-8f006a961fa6.png align="center")

Imagine you have different toys scattered all over your room. It can be difficult to keep track of them and they might get mixed up or interfere with each other. Now, imagine you have a separate container for each toy. Each container keeps the toy and its parts organized, separate from other toys. This way, you can easily manage, move, and play with each toy without any mess or interference.

Each service, such as a web server, database, messaging system, or any other component of the application, is typically deployed and managed within its own container. By running different services in separate containers, you gain several benefits such as process level isolation that is any changes such as a version update for one service do not impact the other services.

## Let us understand how an application run in docker!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987923066/588e907d-031a-4509-a99b-9f3639a4b3de.png align="center")

1. Creating a Docker Image: The application's code, dependencies, libraries, and configurations are bundled together in a Docker image. The image serves as a blueprint or template for running the application.
    
2. Running a Docker Container: Using the Docker image, a Docker container is created. A container is an isolated and lightweight runtime environment that runs the application. It contains the necessary resources and settings to execute the application.
    
3. Container Isolation: The Docker container operates in isolation from other containers and the host system. It has its own file system, network interfaces, and process space. This isolation ensures that the application runs without interference from other containers or the host.
    
4. Container Startup: When the Docker container starts, it executes the commands specified in the image or provided during container creation. These commands typically include setting up the environment, launching the application, and configuring any necessary services.
    
5. Application Execution: Once the container is up and running, the application within the container runs just like it would in any other environment. It can interact with the underlying operating system and utilize the resources allocated to the container.
    

## so we can say that images are stored in a container, when we run the container, it runs that image?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685988046897/ac4a3eb1-c9e3-4352-ab4b-67df0843deca.png align="center")

No, images are not stored in a container. Images and containers are separate entities in Docker.

An image is a static, immutable package that contains the application code, dependencies, and configuration settings. It is a file system snapshot that serves as a blueprint for creating containers. Images are stored in a Docker registry, such as Docker Hub or a private registry.

On the other hand, a container is a running instance of an image. When you run a container, Docker uses the specified image as a base to create a runtime environment for the application. The container includes a writable layer that allows the application to write data and make temporary changes during its execution. However, the image itself remains unchanged.

To create a container, you specify which image to use using the docker commands, and Docker runs a container based on that image.

## Let us understand docker, container and images with an analogy.

You can think of Docker as a ship that carries containers, each encapsulating its own set of dependencies and running independently from each other, but collectively serving the functionality for the same application.

In this analogy, the Docker image represents the cargo that contains all the necessary dependencies, libraries, and configurations required for the application. The Docker image is created and loaded onto the Docker ship.

When the Docker ship sets sail and runs, it creates and manages multiple containers. Each container is like a separate compartment on the ship, isolated from others. Each container runs its own instance of the application, utilizing the resources provided by the Docker ship.

Just as containers on the ship are independent and self-contained, Docker containers are isolated and independent runtime environments for running applications. They have their own file systems, network interfaces, and process spaces. However, they all share the same base image (cargo) from the Docker ship (platform).

This way, Docker enables the efficient and consistent deployment of applications, with each container running its part of the functionality while leveraging the shared dependencies provided by the Docker image.

So, the Docker ship (platform) carries and manages the containers (compartments) that encapsulate the application's dependencies, running independently but working together to provide the complete functionality of the application.

## How exactly is an image created?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685987869658/e139c45a-d4ed-428a-b7c5-e3d177c026ca.jpeg align="center")

1. Image Creation: To create an image, you define a Dockerfile, which is a text file that contains instructions on how to build the image. The Dockerfile specifies the base image, the application code, and any additional dependencies or configurations required.
    
2. Image Build: You use the Docker CLI (Command Line Interface) or Docker build commands to build the image based on the Dockerfile. During the build process, Docker executes the instructions in the Dockerfile and generates an image.
    
3. Image Storage: Once the image is built, it can be stored in a Docker registry. The registry acts as a centralized repository for images and allows for easy sharing and distribution of the image.
    

## is docker like a hypervisor in VM?

No, Docker is not like a hypervisor in virtual machines (VMs). Docker uses a different approach called containerization, which is distinct from the hardware-level virtualization used by hypervisors in VMs.

Hypervisors provide full hardware-level isolation, allowing multiple VMs to run different operating systems with their own kernels. Each VM runs on a virtualized hardware platform, including virtual CPUs, memory, and storage. VMs require emulating a complete hardware stack, including the operating system, which incurs significant overhead in terms of memory usage, disk space, and startup times.

In contrast, Docker containers share the host system's kernel and resources, providing process-level isolation. Containers are more lightweight and have a lower overhead compared to VMs. Containers leverage the host system's kernel, resulting in faster startup times, reduced resource consumption, and improved performance.

## Can docker run any os if they are not based on the same kernel of the host?

No, Docker containers are not capable of running any operating system if they are not based on the same kernel as the host. Docker containers share the host system's kernel and utilize its functionality for resource management and isolation.

This limitation means that Docker containers can run different distributions or versions of Linux operating systems, as long as they share a compatible kernel. However, Docker containers cannot directly run operating systems based on different kernels, such as Windows or macOS.

## How does an application run in docker?

1. Creating a Docker Image: The application's code, dependencies, libraries, and configurations are bundled together in a Docker image. The image serves as a blueprint or template for running the application.
    
2. Running a Docker Container: Using the Docker image, a Docker container is created using the Docker commands on the terminal. A container is an isolated and lightweight runtime environment that runs the application. It contains the necessary resources and settings to execute the application, it is basically a running instance of an image.
    
3. Container Isolation: The Docker container operates in isolation from other containers and the host system. It has its own file system, network interfaces, and process space. This isolation ensures that the application runs without interference from other containers or the host.
    
4. Container Startup: When the Docker container starts, it executes the commands specified in the image or provided during container creation. These commands typically include setting up the environment, launching the application, and configuring any necessary services.
    
5. Application Execution: Once the container is up and running, the application within the container runs just like it would in any other environment. It can interact with the underlying operating system and utilize the resources allocated to the container.
    

## Disadvantages of Docker

1. Docker is not a good solution for application that requires rich GUI.
    
2. Docker does not provide platform compatibility. This means if the application is designed to run in a docker container on Windows then it can't run on Linux or vice versa.
    
3. The docker is suitable when the development O.S. and testing O.S. same. If OS is different we should run VM.
    
4. No solution for data recovery and backup.
    

## Conclusion

In conclusion, we have covered the fundamentals of Docker, containers, and images. Stay tuned for our next blog, where we will unravel the complexities of containerization and VMs, empowering you to optimize your infrastructure and revolutionize your application delivery process. We will explore the advantages, distinctions, and practical use cases of each approach, equipping you with valuable insights to make informed decisions about your application deployment strategies. Feel free to join us as we continue our exploration of containerization versus VMs in our upcoming blog.

### **Check out socials**

[Twitter](https://twitter.com/Karthikreincar1)

[Github](https://github.com/karthiknadar1204)

[LinkedIn](https://www.linkedin.com/in/karthik-nadar-b2155a25b/)