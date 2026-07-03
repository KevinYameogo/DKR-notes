# Why Docker?

1. **_Environment reproducibility_**: Everyone gets the exact same setup.

2. **_Dependency management_**: No Python hell, Conda weirdness, or OS-specific issues.

3. **_Portability_**: Run your container on any machine with Docker (dev laptop, server, cloud instance).

4. **_Version control for environments_**: Dockerfiles are text, making them fully versionable in Git.

# Compute Device components

1. **_Central Processing Unit (The Brain)_**: Is involved in all operations that run on the compute device.

2. **_Random Access Memory (RAM)_**: Used to run applications and hold data during processing.

3. **_Hard Disk Drives (HDD) and Solid-State Drives (SSD)_**: Used to provide persistent storage for OS, Data, and Applications.

4. **_Network Interface Cards_**: Connect the computing device to the outside world. Can be wireless (WiFi) or wired (uses Ethernet/LAN cables).

5. **_Graphic cards or GCPUs_**: Used to accelerate video operations (gaming, rendering) on the compute device. Can be built-in or a card.

# What is a Server?

- A server is basically a powerful computing device with:

- A good size memory (RAM)

- One or more CPU(s)

- One or more disk drives to persistently store the operating system, applications, and data

- One or more network interfaces

- One or more GCPUs

- An operating system (Windows, Linux, or MacOS)

# Server hosting in Datacenters

- A data center is an air conditioned, secure, and monitored space

# Server Resource Optimization & Multiple Apps on a Server

- To optimize resource usage, multiple applications could be run on the same physical server

- Each application may require its own runtime version, dependencies, database..etc

Drawbacks:

- Resource contention and inefficiency

- Dependency conflicts

- Lack of strong isolation - Security risks

- Scaling is painful

- Deployment & maintenance hell

- Lack of portability

# Introduction to virtualization

virtualization introduced isolation, flexibility, scalability, portability.

- Split physical server into multiple virtual servers

- It allows us to run multiple virtual machines,multiple OS and multiple apps on a single physical server

- The "hypervisor" shares the physical server resources among the virtual machine(VMs): vCPU, vRAM, vNIC, vDisk

- Each VM will be given what it needs for its operating system, know as "guest OS"

# Popular Hypervisors Providers

VMware vSphere

Xen

Microsoft Hyper-V

Linux KVM

Oracle VM VirtualBox

VMware Workstation

# Virtual machine issues

Heavyweight (slow to start)

Limited Scalability

Poor Dev/Test/Prod parity

Redundant OS overhead

Inefficient Image Management

Low portability

# A process

A process is a running instance of a program that has its own cpu context, memory, and system resources.

what happens when you run a program (like bash, nginx, or python):

1. Loads the program's code into memory

2. Allocates it a unique Process ID (PID)

3. Creates a process to execute the code

# Containers

A container is a lightweight, isolated process running on a shared operating system kernel, packaged with everything it needs to run, including code, libraries, environment variables, runtime, and configuration files.

- We can run applications inside containers

# Containers feature

Does not require a separate OS

Isolated, self-contained environments

Faster to create and tear down

Repeatable

Portable

Easily scalable

# Containeration overview

To build, ship and run containers, we need a **_container runtime engine_** be installed on the host's operating system

- The engine shares the Host's OS kernel among the containers

- Containerized applications are "isolated"

- Docker is the most popular container engine

It comes in Community Edition (CE) which is free and a paid Enterprise Edition (EE)

# Docker Containers - From a Dockerfile to an Application

Starting with a Dockerfile, we can build a container image that can be used to consistently run an application across different environments.

Container Image can be used mutiple times

![](/public/Screenshot%202026-06-22%20at%203.02.40 PM.png)

- We can run containers on VMs

![](/public/Screenshot%202026-06-22%20at%203.25.19 PM.png)

# Popular Container engines and runtimes

Docker

Linux containers – LXC (System Level containerization framework)

Containerd – geared towards Kubernetes deployments

CRI-O – geared towards Kubernetes deployments

# Docker Architecture - Overview

Docker is a software platform that simplifies the process of building, running, managing, and distributing applications using containers.

Developed by Docker Inc.

Docker is open source

Docker virtualizes the host OS (containers use the same kernel)

Applications run in containers as isolated environments

There are two types of Docker Editions: docker-CE, docker EE

# Docker client

It enables developers/users to interact with Docker

When you use docker commands, the docker client sends these commands to the Docker daemon (dockerd)

# Docker Host

The server or Virtual machine on which Docker Engine is installed

Docker daemon(dockerd) is the heart of Docker.

# Docker images

Images are read-only binary templates used to build containers

They contain the application code, libraries, and dependencies required to run an application

# Docker Daemon

- The Docker Daemon (dockerd) is the heart of Docker

- It listens to Docker API requests (from the Docker client) and manages containers, images, networks, and volumes

- It builds container images as requested by the client

- It interfaces with docker registries to pull or publish images as requested by the client

- It manages the lifecycle of the containers (start, stop, remove)

# Docker Containers

Containers are encapsulated environments in which you run applications

A container is an instance of a Docker image

A container runs as a process in an isolated environment

It packages the application and its dependencies into a single executable unit

# Docker Registries

A Docker registry stores Docker images

Docker Hub is the public registry that anyone can use

When needed, the required images can be pulled from the configured registry

Users can push their created images to the configured registry

![](/public/Screenshot%202026-06-22%20at%206.43.32 PM.png)

![](/public/Screenshot%202026-06-23%20at%206.21.18 PM.png)

# Understanding How Docker Works

Docker CLI

- Docker CLI communicates with the Docker Daemon/server, dockerd

dockerd.

- dockerd processes the Docker API requests and utilizes containerd functionality to manage the container's lifecycle.

Containerd

- Manages containers, Storage, and Networking

- Pushes and pulls images

runC

- Creates and runs containers.

![](/public/Screenshot%202026-06-23%20at%206.39.16 PM.png)

# IAM

- Identity and Access Management

- It is recommended to create a user through IAM and use it for day to day work

- download .csv files for credentials or email it

# Hands-on-Labs

- Launch an AWS EC2 instance

- Ubuntu Linux (wont cost a lot on AWS)

# Launch an AWS ubuntu EC2 Instance - Steps

Open the AWS console

Launch a new Ubuntu EC2 instance (Virtual machine)

Configure the security Group, Allow - All Traffic inbound

Create roles first:

- We will create a AEC2roleforssm first(we called the role: IAMDocker)

- Without IAM role we cant create the VM

- Attach IAM role to instance to be able to communite with SSM

- Connect to Session Manager

- Or connect to EC2 instance connect

# Install docker on our EC2 instance

https://docs.docker.com/engine/install/ubuntu/

run : systemctl enable docker (it will start by itself after every reboot)

- docker info

- cd /var/lib/docker (dont touch anything here)

- ls

# Basic docker commands

## docker pull

docker = dockerd

Syntax : docker pull [OPTIONS] IMAGE[:TAG|@DIGEST]

Download a docker image from a registry (default is Docker Hub) :TAG Specific version

ex:

docker pull ubuntu -> Pulls the latest version of the image ubuntu

docker pull ubuntu:20.04 -> Pulls version 20.04 of the image ubuntu

docker pull --all-tags ubuntu -> Pulls all versions(tags) of the image ubuntu

## docker images

Syntax: docker images [OPTIONS]

List the available Docker images on the local Docker host.

docker images -> List all images on the local host.

docker images -q -> List all the available image IDs.

## docker ps

Syntax: docker ps [OPTIONS]

List the running containers on the Docker host.

It provides detailed information about each container's status, including its ID, name, status, and more.

docker ps -> List the running Docker containers on the system.

docker ps -a (or --all) -> List all containers (both running and stopped).

https://hub.docker.com/

## Docker create

Syntax: docker create [OPTIONS] IMAGE [COMMAND] [ARG...]

Create a container in a stopped state (does not start it).

docker create --name my-container nginx -> Create a container where its name is my-container and the image is nginx.

If the image is not available locally, it will attempt to download it from Docker Hub.

docker create --name my-container ubuntu:20.04 --> Creates a container where its name is my-container and the image is ubuntu release 20.04.

## Docker start

Syntax: docker start [OPTIONS] CONTAINER [CONTAINER...]

Start an already created container that is not running.

CONTAINER refers to the name or ID of the container you want to start.

docker start my-container -> Start the specified container (by name).

docker start abc1234 -> Start the specified container (by ID).

docker start container1 container2 ... -> Start multiple containers at once.

## Docker stop

Syntax: docker stop [OPTIONS] CONTAINER [CONTAINER...]

Stop a running Docker container gracefully.

f the process doesn't terminate within a certain timeout period (by default 10 seconds), it will be forcefully stopped.

docker stop my-container -> Stop the container named my-container

docker stop -t 30 my-container -> Stop the container named my-container and allow it 30 seconds to stop gracefully.

docker stop container1 container2

## A container is a software process

Syntax : ps [OPTIONS]

ps a -> Show processes for all users (not just yours)

ps -A -> Show all processes

ps x -> Show processes not attached to a terminal (e.g., background services)

ps u -> Show process owner (user) and display in user-friendly format

ps aux | grep cont1

## docker exec

Syntax: docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

- Used to execute a command inside a running Docker container.

- It can be used to interact with a container's file system, processes, and environment.

docker exec my-container ls /usr/src/app

Run the "ls" command inside the container my-container to list the contents of the /usr/src/app directory.

Use it with non-interactive commands that do not expect user input like ls, cat, echo.

## docker exec : -t Option

docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

docker exec -t my-container ls /app

This command allocates a terminal (tty) to run interactive commands (like bash) within the container.

- The --tty (or -t) flag attaches a pseudo-TTY to the container.

- Hence, you get access to the input and output features that TTY devices provide.

## docker exec : -i

docker exec -i my-container cat /etc/hostname

i (or --interactive): It keeps the container's Stdin open.

This allows you to send input (commands or else) to the container through the standard input.

Usage Tip: Use it with interactive commands that expect user input like vim, bash, sh, or other applications that require input.

## docker exec -it – Opening a Terminal Inside the Container.

docker exec -it my-container /bin/bash

The two flags (-i and -t) are frequently used together to bind the I/O streams of the container to a pseudo-terminal, creating an interactive terminal session.

/bin/bash specifies the type of shell you want to use(options bash, sh, Zsh etc).

docker exec -it my-container cat /etc/shells

Use this specific command to find out exactly which shells are available for your container.

docker rm cont1 will remove container (id works too)

docker rmi [imageName] to remove images

## docker run

Syntax: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Create and start a container from a specified image in a single step.

docker run nginx -> Create and start a container using the latest nginx image

docker run --name cont1 ubuntu:20.04 -> Create and start a container from the ubuntu:20.04 image and assign it a name cont1.

docker run -d nginx -> Create and start a container from image nginx in the background.

-d: detached mode

## docker run -it options

docker run -it ubuntu /bin/bash -> Create and run an Ubuntu container and open an interactive shell of type Bash.

The container will run in interactive mode with a pseudo-TTY.

The command will also enter the shell (will move to the container prompt).

docker run -it ubuntu bash -> This will do the exact same thing if the bash shell is included in the container $PATH.

![](/public/Screenshot%202026-06-25%20at%208.33.44 PM.png)

## docker run --rm Options

docker run --rm ubuntu echo "this will self-destruct" -> Create and run an Ubuntu container, echo the sentence "this will self-destruct", then delete the container.

Use it for one-off containers such as testing (curl, ping, etc.).

Do not use for long-term containers (websites, databases, etc.).

docker run -it --rm ubuntu bash -> Create and run an Ubuntu container, open an interactive shell into the container.

Behavior: Once the user exits from the shell, delete the container automatically.

docker rm -f my-container -> stop and remove container even if it is running

docker rmi -f my-image force remove image that has dependent containers create from it.

docker rm cc3 (first 3 letter of container)

## docker inspect

Syntax: docker inspect [OPTIONS] OBJECT [OBJECT...]

Use to retrieve detailed, low-level information about containers, images, volumes, or networks in JSON format.

You can run docker inspect on both running and stopped containers.

docker inspect my-container -> Returns: Detailed information about the container (name, ID, Network, Config...)

docker inspect nginx:latest -> Returns: Information about the image named nginx with the latest tag, including: Image ID, Creation time and more.

## docker logs

Syntax : docker logs [OPTIONS] CONTAINER

Use to retrieve the logs of a container.

This can be helpful for troubleshooting, debugging, and monitoring the output of processes running in a container.

docker logs my-container -> Returns: Print the logs of the container named my-container.

docker logs -f my-container -> Returns: Display the logs and keep updating the terminal with new log messages as they are written.

## docker --help

Syntax: docker --help

Description: Display the help documentation for Docker, including the list of available commands and their descriptions.

docker run --help -> Description: List of available options and flags for the docker run command.

## docker image prune

Syntax: docker image prune [OPTIONS]

Description: Remove unused docker images on the host to free up space.

# Docker files

Dockerfile is a text document that contains all the commands a user could use manually on the CLI to build an application

Docker can build images automatically by reading the instructions from a Dockerfile

The command "docker build" reads the instructions in a docker file and creates a docker image

## Docker file strucuture - FROM

The FROM instruction will set the base image for the Dockerfile

Every Dockerfile instruction that follows FROM applies to this base image.

Syntax : FROM <image>[:tag]

Example: FROM ubuntu -> Pull the latest base Ubuntu image

## Docker image layers

The docker image consists of layers

- Each layer maps to a docker instruction in the docker file

![](/public/Screenshot%202026-06-27%20at%209.56.17 PM.png)

## Docker file strucuture - RUN

RUN - runs one or more commands

The RUN instruction will execute any commands in a new image layer and commit the results.

Syntax : RUN <command>

RUN apt-get update

RUN apt-get install –y vim

## Optimizing Image Layers(Recommended)

It is possible to perform multiple commands using multiple lines with a single RUN statement.

This will result in a few image layers

RUN apt-get update

RUN apt-get install –y vim

RUN apt-get update && apt-get install –y \ vim \ git

Will add one layer in the resulting image - Recommend

## Inspecting Image Layers - docker history command

docker history < image name >

use this command to display image layers and their details

## Docker file strucuture - CMD (inside the container)

CMD - specifies the default command to execute when a container starts.

The instruction can provide a default executable, or it can omit the executable if an ENTRYPOINT instruction is specified.

Unlike the RUN instruction, which executes commands during the image build process, CMD is only executed when a container is instantiated from the image.

Syntax : ["executable","param1","param2"]

CMD["python","app.py"] -> at container start, execute "python app.py"

RUN is at build time(adds layers to images, used to install apps) and CMD at runtime(runs command inside container).

## docker build command

Syntax: docker build [OPTIONS] PATH | URL | -

PATH: The build context — usually the current directory.

OPTIONS: Flags you can pass to customize the build.

Dockerfile: By default, Docker looks for a file named Dockerfile, but you can specify a different one.

docker build -t myapp . (-t means tag)

Explanation: Build the image myapp from the dockerfile in the current directory. The current directory is the build context.

## docker build command - Different file name

docker build -f files/test.txt -t image3 /imagefiles

(-f here stands for file and -t tag(name))

Build the image myapp from the test.txt file in the /files directory

The /imagefiles directory is the build context (any build files need to be here)

relative docker build -f /home/ubuntu/apps/imagefiles/test.txt -t image3 /home/ubuntu/build/contextfiles/app1

The build context is needed so Docker can access things like:

source code (app.py, package.json)

config files

dependencies

anything you COPY or ADD in the Dockerfile

//

nano or vim a dockerfile

cat Dockerfile

control + k to delete a line in nano

ex:
FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y git
CMD ["echo", "a ubuntu container with vim and git installed"]

-y means “yes automatically”, it auto-confirms prompts like “Do you want to continue? [Y/n]”

## Docker File Structure - EXPOSE

The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime.

EXPOSE <port>

EXPOSE 80 -> Exposes port 80 or http

EXPOSE 80 443 -> Exposes ports 80 and 443 (HTTP and HTTPS)

EXPOSE is informational only; it does not actually publish or expose the port or open it to the host

You still need to publish the port(s)

It is useful for tools that auto generate configurations (Docker Compose, Swarm, K8s)

## Docker File Structure - COPY

The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.

It can copy files from the build context only (cannot copy files from anywhere)

Syntax: COPY <src> <dest>

COPY app/utils /app/code/utils

# Copy only the 'app/utils' directory to /app/code/utils inside the image

COPY app/main.py /app/code/

# Copy just the app/main.py file into /app/code

### map port 80 on the host to port 80 on the container:

docker run -p 80:80 imageexp (doing publishing your self)

0.0.0.0:80->80/tcp, [::]:80->80/tcp (first is ipv4 and second ipv6)

http:(public ipdress):portNumber to see on the web

# Docker Files - WORKDIR, ENV, LABEL Instructions

## Docker File Structure - WORKDIR

Syntax: Syntax : WORKDIR </path>

WORKDIR is used to define the working directory of the docker container at any given time

It creates the directory specified by “path” and runs all the following container commands (RUN, CMD, ADD, COPY..etc) into this directory

WORKDIR /app -> "Create this directory /app in the image and any container when it is created from the image"

This </path> is a container path, not a docker host path

The </path> will be in the resulting image during build time and in the container during runtime

![](/public/Screenshot%202026-06-30%20at%202.41.11 PM.png)

## Docker File Structure - ENV

The ENV instruction allows for setting environment variables for the Docker container.

Syntax: ENV <key> <value>

ENV name=DolfinED
CMD ["echo", "$name"]

Output: DolfinED

![](/public/Screenshot%202026-06-30%20at%203.15.47 PM.png)

## Docker File Structure - LABEL

The LABEL instruction in Docker is a way to add metadata to an image.

This metadata can include information about the image such as the author, version, description, environment, or other custom data.

Syntax: Syntax : LABEL key="value"

LABEL Owner="DolfinED Academy Team <team@support.dolfined.com>"

# Docker images and Docker registry

![](/public/Screenshot%202026-07-01%20at%208.07.03 PM.png)

Docker registry- pushing images

## Docker Image Naming Convention

Docker Hub has a specific naming convention for Docker images that helps with organization, versioning, and discovery.

[registry/][username_or_org/]repository[:tag]

Registry: (Optional) the domain of the container registry – default to docker.io

Username or organization: The name of the user or organization (required for non-official images only)

Repository: the name of the image or the project

Tag (Optional): The version – defaults to Latest if not included

## Image Rename – docker tag Command

The docker tag command is used to add a new name (or alias) to an existing Docker image (add a custom name to an image).

Syntax : docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

Example Given: docker tag python:3.10 my-python-app:latest

## Docker Registry – docker tag Command

Images must be correctly tagged with the intended registry & image name before they are pushed"

Syntax : docker tag SOURCE_IMAGE REGISTRY_HOST/USERNAME/REPO:TAG

docker tag myapp registry.mycorp.com/devops/myapp:1.0.0

This will tag the image myapp with the name registry.mycorp.com/devops/myapp:1.0.0 in preparation to be pushed to the private registry registry.mycorp.com, under account devops, under repo/image myapp with the tag 1.0.0

## Docker Registry – docker login Command

You have to login to Docker Hub to push to a repository

Syntax: docker login Registry_Host

## DockerHub Registry – docker tag Command

For Dockerhub, you do not need to specify the registry as it defaults to docker.io

The local image name and the repo name can be the same (they do not have to)

Syntax: docker tag LOCAL_IMAGE_NAME:tag USERNAME/REPO:TAG

ex: docker tag myimage myusername/myapp:latest

ex: docker tag myimage myusername/myapp:v1

## Docker Registry – docker push Command

docker push uploads a locally tagged image to a Docker registry (like Docker Hub, GitHub Container Registry, AWS ECR, etc.)

Syntax : docker push [REGISTRY_HOST]/USERNAME/REPO:TAG

[REGISTRY_HOST] is the Registry, USERNAME is the User/Account, and REPO is the Imag/Repo.

Example:

Docker Hub : docker push myapp myusername/myapp:latest

Generic Registry : docker push registry.mycorp.com/devops/myapp:1.0.0

compress: tar -czvf archive.tar.gz test.txt

docker login -u princier77

# Docker networking overview

## Network Bridges - Overview

A bridge is a data link-layer (OSI layer 2) physical or virtual device that forwards traffic between two or more network segments.

## Docker Bridge Networks

In Docker, a bridge network uses a software bridge to allow containers to communicate inside the docker host.

By default, when you start Docker, a bridge (docker0) is created automatically.

## Docker Network Modes (Drivers)

Bridge (default) - The default network driver.

Host - Remove network isolation between the container and the Docker host.

None - Completely isolate a container from the host and other containers.

Overlay - Overlay networks connect multiple Docker daemons together.

Ipvlan - Ipvlan networks provide full control over both IPv4 and IPv6 addressing.

Macvlan - Assign a MAC address to a container.Userdefined — Custom network

## Bridge Driver / Mode

Containers connected to the same bridge network can communicate.

A bridge network isolates its containers from other containers on other bridges.

Bridge networks apply within the same Docker host only.

A container can connect to multiple bridge networks at the same time.

![](/public/Screenshot%202026-07-02%20at%203.29.14 PM.png)

## Docker Default Bridge (docker0)

The default docker bridge network (docker0) IP subnet is 172.17.0.0/16.

172.17.0.1 is the IP default gateway between bridge Docker0 and the Docker host.

Unless otherwise specified, all newly created containers attach to Docker0.

Each container created in bridge mode has an eth0 with an assigned IP address.

A new bridge virtual interface (veth) is created with every running container.

![](/public/Screenshot%202026-07-02%20at%203.39.52 PM.png)

## Bridge Mode - Containers Outbound Connectivity To External Networks

In bridge network mode, when a container communicates outbound with external networks, the Docker host performs Network Address Translation (NAT).

The Docker host maintains NAT entries in IPtables.

![](/public/Screenshot%202026-07-02%20at%203.46.54 PM.png)

## Bridge Mode – Multiple Bridge Networks

Multiple bridge networks can co-exist inside a docker host.

We can create custom bridge networks as needed (aside from the default bridge).

A bridge network isolates its containers from other containers on other bridges.

![](/public/Screenshot%202026-07-02%20at%203.55.16 PM.png)

# Docker networking commands

ip a —> Display network interfaces and their associated IP addresses on a Linux-based system.

docker network ls —> List all available networks.

docker network create <name> —> Create a new network with a specific name.

docker network create --subnet 10.0.0.0/16 <network-name> -> Create a new network with a custom subnet range.

docker network inspect <network-name or ID> —> Inspect a docker network.

docker run --network <network-name> <image-name> —> Run a new container and connect it to a Docker network.

docker network connect <network-name> <container_name> —> Connect a running container to a Docker network.

docker network disconnect <network-name> <container_name> —> Disconnect a running container from a Docker network (Does not work with none and host network modes).

apt-get install -y iproute2

# Persisting data in Docker

### The need for persisting data in docker containers

Data in a container is lost if a container is deleted

# Persisting Data in Docker - Benefits

Persist data (e.g., database files, logs)

Share data between containers

Separate app code from user data

Avoid losing data when a container stops or is deleted

The Two Common Ways to Persist Data in Docker Containers:

Volumes

Bind Mounting

# Docker volumes

Volumes are stored in the host filesystem in the Docker internal storage area which is managed by Docker.

Each volume gets its own volume path as follows: /var/lib/docker/volumes/<volume-name>/\_data/

Is isolated from container layers

Persists independently of containers

Is mounted into containers at runtime

It allows data to survive container restarts, deletion, and image rebuilds

# docker volume commands

docker volume create <volume-name> — Create a new "named" docker volume

docker volume ls — List existing docker volumes

docker volume inspect <volume-name> — Show detailed info about a volume

docker volume rm <volume-name> — Delete a docker volume

-v [volume name]:[container directory]

Launch a container with a volume attached

docker run -v mydata:/app/data ubuntu

Create an ubuntu container and a volume mydata.
Mount the volume at the /app/data folder in the container

-v [volume name]:[container directory]:ro

Launch a container with a read-only volume attached

docker run -v mydata:/app/data:ro ubuntu

Create an ubuntu container and a volume mydata.
Mount the volume at the /app/data folder in the container.
The container has read only access to the mydata volume

## Sharing Data Between Multiple Docker Containers

The --volumes-from flag allows you to inherit all the volume mounts from another container.

It is not as common today.

--volumes-from container1

--volumes-from container1:ro

docker run -it --volumes-from cont1 ubuntu

Create an ubuntu container and allow it to inherit all volume mounts from cont1
