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

```python
name
```
