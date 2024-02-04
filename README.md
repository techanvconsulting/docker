# Docker Podman Notes

# Running Ubuntu as a Docker Container

## Introduction

Explore the efficient deployment of Ubuntu as a Docker container, a lightweight alternative to traditional virtual machines. Docker, a widely acclaimed programming tool, has significantly streamlined the process of application deployment through containerization.

**Author:** Viral Jain
**Reading Time:** 11–14 minutes

## Table of Contents

- [Docker Podman Notes](#docker-podman-notes)
- [Running Ubuntu as a Docker Container](#running-ubuntu-as-a-docker-container)
  - [Introduction](#introduction)
  - [Table of Contents](#table-of-contents)
  - [Getting Started](#getting-started)
    - [Step 1: Obtaining the Ubuntu Docker Image](#step-1-obtaining-the-ubuntu-docker-image)
    - [Step 2: Running the Ubuntu Docker Image](#step-2-running-the-ubuntu-docker-image)
  - [Working with Ubuntu in Docker](#working-with-ubuntu-in-docker)
    - [Executing Linux Commands](#executing-linux-commands)
    - [Preserving the Docker Container State](#preserving-the-docker-container-state)
    - [Persisting Data on the Ubuntu Docker Container](#persisting-data-on-the-ubuntu-docker-container)
  - [Summary](#summary)
  - [Conclusion](#conclusion)

## Getting Started

### Step 1: Obtaining the Ubuntu Docker Image

If Docker is not installed, please refer to our [guide on installing Docker on Ubuntu](#). Docker Hub is the recommended repository for official Docker images. Download the latest Ubuntu Docker image:

```bash
sudo docker pull ubuntu
```

For a specific version:

```bash
sudo docker pull ubuntu:20.04
```

List all Docker images:

```bash
sudo docker images
```

### Step 2: Running the Ubuntu Docker Image

Run the downloaded image in interactive terminal mode:

```bash
sudo docker run -ti --rm ubuntu /bin/bash
```

Explore the lightweight Ubuntu container, devoid of a graphical user interface (GUI) and unnecessary tools.
This command tells Docker to run the Docker Ubuntu container in an interactive terminal mode (-ti). The /bin/bash argument is a way of telling the container to run the Bash shell terminal. Finally, the --rm flag instructs Docker to automatically remove the Ubuntu Docker container after we stop it.

## Working with Ubuntu in Docker

### Executing Linux Commands

Execute Linux commands inside the Ubuntu Docker container. For example:

```bash
cat /etc/os-release
```

Install additional packages as needed:

```bash
apt update && apt install lsb-core
```

### Preserving the Docker Container State

Save changes made to the container:

```bash
sudo docker ps
sudo docker commit -p container_id myubuntu
```

Create a custom Docker image named "myubuntu" with the changes.

### Persisting Data on the Ubuntu Docker Container

Utilize Docker's data persistence features:

```bash
sudo mkdir -p Docker_Share
sudo docker stop container_id
sudo docker run -ti --rm -v ~/Docker_Share:/data ubuntu /bin/bash
```

Access and modify files in the `/data` directory, persisting data between host and container.

```md
# Persisting Data on the Ubuntu Docker Container

One powerful feature of Docker is the ability to persist or share data with the host machine. There are two main options for persisting data:

- Mounted volumes
- Docker volumes

Docker recommends using Docker volumes over mounted volumes.

## Creating a Docker Volume

You can create a Docker volume anywhere on your host machine. Let's create one in the home directory called `Docker_Share`:
```

$ sudo mkdir -p ~/Docker_Share

```

## Stopping the Container

Next, stop the Ubuntu container using the following command. Substitute `container_id` with the actual ID of your Ubuntu Docker container:

```

$ sudo docker stop container_id

```

## Running the Container with the Volume

Finally, we can run the Ubuntu Docker image and mount the `Docker_Share` directory as a volume using this command:

```

$ sudo docker run -ti --rm -v ~/Docker_Share:/data ubuntu /bin/bash

```

Alternatively, you can use a docker-compose file to easily start your containers with mounted volumes.

This will start the Ubuntu image and create the `/data` directory within the container. The `/data` directory is mapped to the `Docker_Share` folder we created earlier.

Any files created or modified in `/data` will now also be accessible in `Docker_Share` on the host, and vice versa.

## Summary

The key points are:

- Docker volumes allow persisting data between the host and container
- Create a Docker volume on the host machine
- Mount it when starting the container using `-v host_dir:container_dir`
- Modifications on either the host or container will be mirrored

## Conclusion

Docker provides a powerful and efficient alternative to virtual machines. Deploying a lightweight Ubuntu Docker container allows for secure application deployment and management. Experiment with Docker to unlock its diverse capabilities.
```
