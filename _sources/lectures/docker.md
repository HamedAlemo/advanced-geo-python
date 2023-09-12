# Introduction to Docker

In this chapter, you will learn about containerization and Docker as one of the platforms for containerization. 

**Attribution**
*The content of this lecture are modified from three excellent sources: [Docker for beginners](https://docker-curriculum.com/); [Introduction to Docker Containers](https://learn.microsoft.com/en-us/training/modules/intro-to-docker-containers/2-what-is-docker) by Microsoft; and [Reproducible Computational Environments Using Containers: Introduction to Docker](https://carpentries-incubator.github.io/docker-introduction/) from Software Carpentry*

## Containerization

In software development and deployment teams, containerization has become a regular practice that allows developers to package applications and their dependencies into lightweight, portable units known as containers. Docker is one of the most popular containerization platforms. 

Containers are self-sufficient units that package an application and all its required dependencies, including libraries and configuration files, into a single image. These containers can run consistently across different environments, ensuring that an application behaves the same way whether it's in a developer's laptop or a production server. Containers do not have high overhead like virtual machine (VM), and hence enable more efficient usage of the underlying system and resources.

## Why Containers?

Containerization has several benefits:

1. **Portability:** Containers encapsulate everything an application needs to run, making it easy to move between different environments without modification.
1. **Consistency:** Containers ensure that the application runs the same way everywhere, eliminating the "it works on my machine" problem.
1. **Isolation:** Containers provide process and resource isolation, ensuring that one container cannot interfere with another, improving security and stability.
1. **Scalability and Speed:** Containers can be easily scaled up or down to meet changing workloads and the speed to deploy them is much higher than VMs. 
1. **Resource Efficiency:** Containers are lightweight and share the host OS kernel, making them more resource-efficient than traditional virtualization. While containers live on top of a host machine and use its resources, they virtualize the host OS unlike VMS that virtulize the underlying hardware. Meaning containers don’t need to have their own OS, making them much more lightweight than VMs, and consequently quicker to spin up.

## What is Docker?

Docker is a leading containerization platform that has played a major role in popularizing containers. Docker is open-source and it provides a set of tools and services for creating, deploying, and managing containers.

## Docker Components
1. **Docker Engine:** The core component of Docker that acts as a client-server application. It includes 
  - Docker daemon (`dockerd`) which acts as the server and responds to requests from the client. 
  - Docker REST API for communication, and 
  - Docker client which has two alternatives: the command line interface (CLI) names `docker` and the graphical user interface (GUI) application named Docker Desktop. 
2. **Images:** A snapshot of a file system with the application code and all dependencies needed to run it. Images are used to create containers.
3. **Containers:** An instance of a Docker image that can run a specific application. Containers are isolated from each other and share the host OS kernel.
4. **Docker Hub:** A registry of Docker images containing all available Docker images ([link](https://hub.docker.com/)). 


```{figure} ../lectures/figures/docker-engine.svg
---
name: docker-engine
class: bg-primary mb-1
width: 700px
align: center
---
Different components of Docker. [source: [Introduction to Docker Containers](https://learn.microsoft.com/en-us/training/modules/intro-to-docker-containers/2-what-is-docker)]
```

## Run Your First Docker Container

There is a simple Docker image that you can run as a container and also verify that your Docker installation is correct. To do this, execute the following the command:
```
$ docker run hello-world
```

## What is a Dockerfile?

A Dockerfile is a text file that contains the instructions we use to build and run a Docker image. The following aspects of the image are defined:

- The base or parent image we use to create the new image
- Commands to update the base OS and install additional software
- Build artifacts to include, such as a developed application
- Services to expose, such as storage and network configuration
- Command to run when the container is launched

**Note**: A *base image* is an image that uses the Docker `scratch` image. The `scratch` image is an empty image that doesn't create a filesystem layer. This image assumes that the application you're going to run can directly use the host OS kernel. A *parent image* is an image from which you create your images. For example, instead of creating an image from `scratch` and then installing Ubuntu, we'll rather use an image already based on Ubuntu. 

## Useful Docker CLI Commands

1. **Build an Image**

    You can use `docker build` command to build a Docker image from a Dockerfile as following:
    ```
    $ docker build -t <NAME:TAG> .
    ```
    This command assumes you have a Dockerfile in the current directory. If your Dockerfile is not in the current directory, or if the file name is not *Dockerfile* you need to replace `.` with `-f <PATH to DOCKERFILE>`. 

1. **List Images**

    You can list all images on your machine using the `docker images` command:
    ```
    $ docker images
    ```
    The output will be a table similar to the following (this is from Hamed's computer!):
    ```
    REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
    giswqs/segment-geospatial   latest    cd7db75a587c   3 weeks ago    5.34GB
    gfm-gap                     latest    93ca820ec782   2 months ago   2.73GB
    cdl                         latest    9f1e0f6b1273   2 months ago   2.73GB
    hls                         latest    1d3452e331df   2 months ago   9.73GB
    lc-td                       latest    221b2866cb63   3 months ago   1.82GB
    ```

1. **Remove an Image**

    You can remove an image using the `docker rmi` command. This can be used to free some space on your computer. You can specify the name or ID of an image as following (including the tag is optional):
    ```
    $ docker rmi <IMAGE ID or NAME:TAG>
    ```

1. **Run a Container**

    You can run a container using the `docker run` command. You only need to specify the Docker image name or ID to launch a container from the image. 
    ```
    $ docker run <IMAGE ID or NAME:TAG>
    ```

1. **List Available Containers**

    You can use `docker ps` to list containers in *running* state. To see all containers in all states, pass the `-a` flag to the command:
    ```
    $ docker ps -a
    ```

    *To learn more about Docker container states, check out this [page](https://learn.microsoft.com/en-us/training/modules/intro-to-docker-containers/4-how-docker-containers-work).*


1. **Interrupt a Container**
    
    You can stop or restart a container using one of the following commands:
    ```
    $ docker stop <CONTAINER ID or NAME>
    $ docker restart <CONTAINER ID or NAME>
    ```

1. **Remove a Container**

    You can remove a container using the following command. Note that this will result in all the data in the container to be deleted. 
    ```
    $ docker rm <COTAINER ID or NAME>
    ```


## Create Your Own Dockerfile
You can create your own Dockerfile with specific software and packages installed. This is a nice way to create a reproducible and portable runtime environment for your projects. 
Here is an example of a Dockerfile:
```
FROM continuumio/miniconda3:22.11.1

# Set the working directory to /home/workdir
RUN mkdir /home/workdir
WORKDIR /home/workdir

# Create a Conda env named 'myenv' with numpy installed in it
RUN conda create -n myenv numpy=1.25.0

CMD ["/bin/bash"]

```

So let's look what each of these commands mean:

**FROM**

Use the FROM command to specify the parent image that you want your image to derive from. Here, we’re using the `continuumio/miniconda3:22.11.1` image.

**RUN**

Use RUN to execute any shell command when the image is being built. Note that this is different from a command you want to execute when running the container. 

**WORKDIR**

Sets the current working directory inside the container (like a `cd` command in shell). All subsequent commands in the Dockerfile will happen inside this directory.

**CMD**

This is the command instruction, it specifies what to run when the container is started. Here we’re simply setting the container run the `bash`.

Other useful commands inside a Dockerfile are:

**COPY**

The COPY instruction has the following format: COPY <source> <dest>. It copies files from <source> (in the host) into <dest> (in the container). This is run at the time that the Docker image is being built, and the copied files are stored in the image (which means the files are not needed to be available when running the container.)



```{Tip}
You can consult this Docker CLI [cheatsheet](https://docs.docker.com/get-started/docker_cheatsheet.pdf) for a quick reference of its most used commands.
```