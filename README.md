<h1 align="center">Docker Cookbook: from Beginner to Advanced</h1>
<p align="center">Be ready always</p>
<p align="center">
    <span>
        <a href="https://github.com/reyadussalahin/docker-cookbook/blob/main/LICENSE">
            <img alt="License" src="https://img.shields.io/github/license/reyadussalahin/docker-cookbook?color=green&style=flat">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cookbook/stargazers">
            <img alt="Stars" src="https://img.shields.io/github/stars/reyadussalahin/docker-cookbook?style=flat&color=magenta">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cookbook/network/members">
            <img alt="Forks" src="https://img.shields.io/github/forks/reyadussalahin/docker-cookbook?style=flat">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cookbook/pulls">
            <img alt="PRs" src="https://img.shields.io/github/issues-pr/reyadussalahin/docker-cookbook?style=flat">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cookbook/issues">
            <img alt="Issues" src="https://img.shields.io/github/issues/reyadussalahin/docker-cookbook?style=flat&color=orange">
        </a>
    </span>
</p>
<hr>
<p align="center">
Docker Cookbook is here to help you with solving from basic to advanced common docker problems. It's a recipe for making docker usage as enjoyable as possible in your daily life.
<hr>


<sub>Connect with me in [linkedin](https://www.linkedin.com/in/reyadussalahin/) or say hi to [Twitter](https://twitter.com/reyadussalahin).</sub>


Introduction
===================
Docker is here to make our life easier, from development to testing and deployment. As we all already know, `Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.` For convenience, I'd still give a brief decription of what is it:

Docker takes advantage of a few linux kernel constructs, one of them is `namespaces` and another one is `cgroups` to provide resource isolation, thus a virtualized environment for processes to run and communicate.

Docker Architecture
-------------------

Docker implements `client/server` architecture to provide facilities to docker use. It consists of the following elements:

1. Docker Daemon: The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

2. Docker client: The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

3. REST API: The REST API acts as a bridge between the daemon and the client. Any command issued using the client passes through the API to finally reach the daemon.

4. Docker registries: A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

The docker architecture is give below:
![Docker Architecture](https://docs.docker.com/engine/images/architecture.svg)


Docker objects
----------------
When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

**Images**

An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run. You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

**Containers**

A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.


Docker Basics
==================

Simple commands
-----------------
```bash
# pull an image from a docker regeistry to local host
docker pull <image-name:tag>

# run a container from an image
docker run <image-name:tag>

# run a container with a preferred name
docker run --name <container-name> <image-name:tag>

# run a container in interactive mode
docker run -it <image-name:tag>

# run a container in interactive mode with a command
docker run -it <image-name:tag> <command>

# run a container in detached more
docker run -d <image-name:tag>

# list running containers
docker container ls

# list of all created containers
docker ps -a

# stop a docker container
docker stop <container-id>

# restart a stopped container
docker start <container-id>

# attach to a running docker container
docker attach <container-id>

# removing a docker container
docker rm <container-id>
```

Executing command from outside
-------------------------
```bash
# executing simple commands
docker exec <container-id> <command>

# examples
docker exec <container-id> echo  "hello, world!"
docker exec <container-id> mkdir /app
docker exec <container-id> ls -la /
```

```bash
# executing interactive commands
docker exec -it <container-id> <command>

# examples
docker exec -it <container-id> /bin/bash
```

Creating docker image from container
-------------------------
```bash
docker commit <container-id> <image-name:tag>
```
Example - Creating a nginx image from a container:

1. First create an ubuntu container
```bash
docker run -it --name ubuntu ubuntu:latest /bin/bash
```

2. Now, inside the container install `nginx`.
```bash
root@container-id > apt-get update && apt-get install nginx -y
# after installation, simply exit
root@container-id > exit
```

3. Then, create an image from the container as follows:
```bash
docker commit <ubuntu-container-id> ubuntu-with-nginx # here's the image name `ubuntu-with-nginx`
```

4. Now, check the image
```bash
docker images
# you'd see ubuntu-with-nginx is listed in the images 
```

5. You can now create a container from the image and run
```bash
docker run -it --name awesome-ubuntu-with-nginx ubuntu-with-nginx /bin/bash
```

6. Now, check if inside the container `awesome-ubuntu-with-nginx` has nginx inside it
```bash
root@container-id > nginx -v
# you'd see nginx version
```




## License
This repository is published under `MIT License`. To know more about license please visit [this link](LICENSE).

## Contributing
I'll continue to improve this repository. So, watch this repo. If you want to contribute, please read [this guide](CONTRIBUTING.md).
