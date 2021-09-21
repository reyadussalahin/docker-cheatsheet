<h1 align="center">Docker Cheatsheet</h1>
<p align="center">Be ready always</p>
<p align="center">
    <span>
        <a href="https://github.com/reyadussalahin/docker-cheatsheet/blob/main/LICENSE">
            <img alt="License" src="https://img.shields.io/github/license/reyadussalahin/docker-cheatsheet?color=green&style=flat">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cheatsheet/stargazers">
            <img alt="Stars" src="https://img.shields.io/github/stars/reyadussalahin/docker-cheatsheet?style=flat&color=magenta">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cheatsheet/network/members">
            <img alt="Forks" src="https://img.shields.io/github/forks/reyadussalahin/docker-cheatsheet?style=flat">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cheatsheet/pulls">
            <img alt="PRs" src="https://img.shields.io/github/issues-pr/reyadussalahin/docker-cheatsheet?style=flat">
        </a>
    </span>
    <span>
        <a href="https://github.com/reyadussalahin/docker-cheatsheet/issues">
            <img alt="Issues" src="https://img.shields.io/github/issues/reyadussalahin/docker-cheatsheet?style=flat&color=orange">
        </a>
    </span>
</p>
<hr>
<p align="center">
Docker Cheatsheet is here to help you with solving from basic to advanced common docker problems. It's a recipe for making docker usage as enjoyable as possible in your daily life.
</p>
<hr>


<sub>Connect with me in [linkedin](https://www.linkedin.com/in/reyadussalahin/) or say hi to [Twitter](https://twitter.com/reyadussalahin).</sub>



Conventions
===============================
1. `iname` means `image name`
2. `cname` means `container name`
3. `vname` means `volume name`
4. `nname` means `network name`
5. `cid` means `container id`
6. `cport` means `port in container`
7. `hport` means `port in host`
8. `cdir` means `directory in container`
9. `hdir` means `directory in host`


Commands
===============================

Image Related
-----------------
```console
$ docker image pull <iname:tag>                                # pulls an image from a registry
$ docker image ls                                              # lists images
$ docker image build -t <iname:tag> .                          # builds an image from Dockerfile in the current directory
$ docker image build -t <iname:tag> -f <path/to/dockerfile>    # builds an image from dockerfile with given path
$ docker image rm <iname:tag>                                  # removes an image
```

Container Related
------------------
```console
$ docker container run <iname:tag>                         # runs a container with an arbitrary name
$ docker container run --name <cname> <iname:tag>          # runs a container with a preferred name 
$ docker container run -it <iname:tag> <command>           # runs a container in interactive mode with a given command
$ docker container run -d <iname:tag>                      # runs a container in detached mode
$ docker container run -dit <iname:tag>                    # runs a container in detached interactive mode
```

```console
$ docker container ls                                      # lists running containers
$ docker container ps -a                                   # lists all(both running and stopped) containers
```

```console
$ docker container stop <cid>                              # stops a container with given container id
$ docker container stop <cname>                            # stops a container with given container name
$ docker container start <cid>                             # restarts a stopped container
$ docker container start <cname>                           # restarts a stopped container
$ docker container attach <cid>                            # attaches a running docker container
$ docker container attach <cname>                          # attaches a running docker container
$ docker container rm <cid>                                # removes a container
$ docker container rm <cname>                              # removes a container
```

```console
$ docker container exec <cid> <command>                    # executes command inside container with given id
$ docker container exec <cname> <command>                  # executes command inside container with given name
$ docker container exec -it <cid> <command>                # executes command inside container in interactive mode
$ docker container exec -it <cname> <command>              # executes command inside container in interactive mode
```

```console
$ docker container run -p <hport>:<cport> <iname:tag>      # publishes a given container port in a given host port
```

```console
$ docker container run -v /path/to/hdir:/path/to/cdir <iname:tag>    # binds a given host dir to a given container dir
```



<!-- Examples -->


<!-- Executing command from outside
------------------------- -->

<!-- ```bash
# executing simple commands


# examples
docker exec <container-id> echo  "hello, world!"
docker exec <container-id> mkdir /app
docker exec <container-id> ls -la /
```

```bash
# executing interactive commands


# examples
docker exec -it <container-id> /bin/bash
``` -->


<!-- Creating docker image from container
------------------------- -->

<!-- ```bash
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
``` -->


<!-- Publishing port
----------------- -->

<!-- Sometimes we need to open a port of a docker container in the host operating system, so that other processes can communicate with the docker container.

```bash
docker run -dit -p <host-port>:<container-port> <image-name:tag>
```

Example:
- Running a nginx container and publish the container's port 80 to host os's 5000 port
```bash
docker run -dit --name nginx -p 5000:80 nginx
```
- Now, you can check if nginx by using the url `http://127.0.0.1:5000/`
or, you may also use curl
```bash
curl 127.0.0.1:5000
# you'll see the nginx welcome page html here
``` -->


<!-- Binding a directory
--------------------- -->

<!-- We can bind a directory of host os with a directory of container using the `-v` flag.

```bash
docker run -dit -v /path/to/host/dir:/path/to/container/dir <image-name:tag>
```

Example:
- Let's create a directory that we want to appear in the container and let it be `./app`
- Also, create a markdown file in it called `readme.md` inside `./app` directory i.e. `./app/readme.md`
- add some content to `./app/readme.md`, such as `echo "# My App"`
- Now, create container from `ubuntu:latest` and share `/usr/src/app` inside the container as follows:
```bash
docker run -dit --name ubuntu -v $(pwd)/app:/usr/src/app ubuntu
```
- Now, go inside the ubuntu container:
```bash
docker exec -it ubuntu /bin/bash
```
- And check if readme exists inside `/usr/src/app` directory as follows
```bash
root@container-id > cat /usr/src/app/readme.md
# you'll see the contents of readme.md here
``` -->


## License
This repository is published under `MIT License`. To know more about license please visit [this link](LICENSE).

## Contributing
I'll continue to improve this repository. So, watch this repo. If you want to contribute, please read [this guide](CONTRIBUTING.md).
