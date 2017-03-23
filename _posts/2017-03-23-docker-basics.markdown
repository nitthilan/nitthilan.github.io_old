---
layout: post
title:  "Docker Basics"
date:   2017-03-23 00:33:14 +0530
categories: Docker, images
---

### Understanding Docker

#### References:
- [Docker for beginners](https://prakhar.me/docker-curriculum/)
- [How To Remove Docker Images, Containers, and Volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)
- [List dependent child images](http://stackoverflow.com/questions/36584122/docker-how-can-i-get-the-list-of-dependent-child-images)

#### Important Commands
- docker run hello-world
    - To test whether installation works fine
- docker pull <docker image>
- docker run busybox - Running busybox image
- docker ps -a - list all running docker instances
- docker run -it busybox sh - run image and open a shell for executing commands
- docker run --help - All variants of run 
- docker rm 305297d7a235 ff0a5c3750b9 - removing running instances of docker
    - docker rm $(docker ps -a -q -f status=exited)
        - remove all the running docker images
- docker port [container] - List of ports exposed by the container
- Run variations
    - docker run -p 8888:80 prakhar1989/static-site
        - mapping container port to external port
    - 
- Image related commands:
	- docker images - list of all docker images
	- docker rmi Image Image - removing images
	- docker rmi $(docker images -f dangling=true -q) - removing all dangling images
	- docker images -f dangling=true - list all dnagling images
	- docker images | grep "pattern" | awk '{print $1}' | xargs docker rm - remove all docker images according to a pattern
	- docker rm $(docker ps -a -f status=exited -q) - remove all exited containers
	- docker inspect --format='{{.Id}} {{.Parent}}' $(docker images --filter since=[image name] -q)
        - Identify all the image dependency for the spcified image

#### Terminology
- Images - The blueprints of our application which form the basis of containers. In the demo above, we used the docker pull command to download the busybox image.
- Containers - Created from Docker images and run the actual application. We create a container using docker run which we did using the busybox image that we downloaded. A list of running containers can be seen using the docker ps command.
- Docker Daemon - The background service running on the host that manages building, running and distributing Docker containers. The daemon is the process that runs in the operation system to which clients talk to.
- Docker Client - The command line tool that allows the user to interact with the daemon. More generally, there can be other forms of clients too - such as Kitematic which provide a GUI to the users.
- Docker Hub - A registry of Docker images. You can think of the registry as a directory of all available Docker images. If required, one can host their own Docker registries and can use them for pulling images.

#### Important Links
- [Repository](https://hub.docker.com/explore/)
- 