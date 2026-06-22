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
