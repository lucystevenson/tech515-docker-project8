# Docker app project 8

<br>
<br>

# Day 1 Install Docker Desktop

Make sure that you have Docker and Docker Compose installed

- Windows or macOS: Install Docker Desktop
- Linux: Install Docker and then Docker Compose

<br>
<br>

# Day 1 Task: Research Microservices, Containers and Docker

This section covers the fundamentals of **virtualisation vs containerisation**, **microservices**, and **Docker**, including benefits, architecture, and real-world usage.

---

## 1. Virtualisation vs Containerisation

### What is Virtualisation?
Virtualisation uses **Virtual Machines (VMs)** to run multiple operating systems on a single physical machine using a **hypervisor**.

### What is Containerisation?
Containerisation packages an application and its dependencies into a **container** that runs on a shared operating system kernel.

---

### What is included?

#### Virtual Machine includes:
- Full guest operating system
- Application code
- Libraries and dependencies
- Virtual hardware
- Hypervisor layer

#### Container includes:
- Application code
- Libraries and dependencies
- Runtime environment
- **Shares the host OS kernel**

---

### Key Differences

| Feature | Virtual Machine | Container |
|------|---------------|-----------|
| OS | Full OS per VM | Shared host OS |
| Size | Large (GBs) | Small (MBs) |
| Startup time | Minutes | Seconds |
| Performance | Slower | Near-native |
| Isolation | Strong | Process-level |

---

### Benefits of Virtual Machines
- Strong isolation and security
- Can run different operating systems on the same host
- Ideal for legacy applications
- Better fault isolation than traditional physical servers

**Compared to traditional architecture (one app per server):**
- Better resource utilisation
- Reduced hardware costs
- Easier backups and snapshots
- Faster provisioning

---

### Benefits of Containers
- Lightweight and fast
- Consistent environments across dev/test/prod
- Easy scaling and portability
- Ideal for microservices

---

## 2. Microservices

### What are Microservices?
Microservices are an architectural style where an application is built as a collection of **small, independent services**, each responsible for a specific business function.

Each service:
- Runs independently
- Has its own database (often)
- Communicates via APIs (HTTP/REST, gRPC, messaging)

---

### How are Microservices Made Possible?
- Containers (Docker)
- Cloud infrastructure
- APIs & RESTful services
- Service discovery
- CI/CD pipelines
- Container orchestration (Kubernetes)

---

### Benefits of Microservices
- Independent deployment
- Easier scaling (scale only what you need)
- Faster development cycles
- Improved fault isolation
- Technology flexibility (different languages per service)
- Better team autonomy

---

## 3. Docker

### What is Docker?
Docker is a **containerisation platform** that allows developers to build, package, and run applications in containers.

---

### Running interactive vs detached containers
Docker runs containers in two ways: interactive mode (-it) and detach mode (-d). Each mode has specific use cases depending on your goals. 

- it: Interactive mode: If you want to work directly inside a container using the terminal, you can use the -it flag. It puts the container in interactive mode, so you can type commands, see the output, and work in real-time.
-i: Keeps the input open so you can type commands into the container
-t: Gives you a terminal-like interface inside the container
- -d: Detached mode: It runs the container in the background, so your terminal is free for other tasks. 

### Docker Alternatives
- Podman
- LXC/LXD
- Containerd
- CRI-O

---

### How Docker Works (Architecture / API)

#### Core Components:
- **Docker Client** – CLI used by developers
- **Docker Daemon (dockerd)** – Manages containers, images, networks
- **Docker Images** – Read-only templates for containers
- **Docker Containers** – Running instances of images
- **Docker Registry** – Stores images (e.g. Docker Hub)

#### Flow:
1. Developer runs a Docker command
2. Docker Client sends API request to Docker Daemon
3. Daemon builds or pulls image
4. Container is created and run

Docker uses a **REST API** internally for communication between client and daemon.

---

### Docker Success Story

#### Netflix
- Uses Docker extensively for microservices
- Enables rapid scaling for millions of users
- Faster deployment cycles
- Improved reliability and fault isolation

Docker allowed Netflix to move from monolithic applications to a highly scalable microservices architecture running in the cloud.

---

## Summary
- **Virtual Machines** provide strong isolation and flexibility
- **Containers** offer speed, efficiency, and portability
- **Microservices** enable scalable, maintainable systems
- **Docker** is the most widely adopted container platform enabling modern cloud-native applications

> Docker command help
> https://docs.docker.com/get-started/docker_cheatsheet.pdf

---

<br>
<br>

# Day 1 Learn to manage Docker containers locally:

## Task: Run and pull your first image

1. Open a Git Bash window (or terminal on Mac)

2. Get help from the docker command

3. Workout the docker command to show all Docker images you already have on your local machine, then run it

4. Run your first Docker container using the `hello-world` image

5. Re-run the command and notice the difference. Does the image need to be downloaded again when the command is run a second time? Document what happens when you run a docker image that does vs does not already exist on your local machine.

6. Well done, you’ve run your first Docker container. Document everything you’ve learnt

How to run Docker?

`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]` - tells Docker to spin up a new container based on an image.

[OPTIONS] - Extra flags to customize how the container runs
IMAGE - The Docker image name 
[COMMAND] - (Optional) Overrides the default command in the image.
[ARG...]- (Optional) Arguments.
- You can pass environment variables using -e parameter. Here’s an example command:
`docker run -e ENV=production -e DEBUG=False my-image` / OR You can create a .env file with all environment variables and pass it to the command `docker run --env-file .env my-image`

sample .env file
```
ENV=staging
DEBUG=True
SECRET_KEY=mysecret
```

- Containers store data temporarily. Once you delete them, the data is gone. A volume is a way to store data outside the container so it persists even if the container is removed or restarted `docker run -v my-volume:/app/data my-image`

How to create custom images and run them?

- Use images from Docker Hub. You can grab pre-built ones or upload yours to share with others. 
- To run a Docker image, you’ll first need to build it using a Dockerfile. Then, you can run it locally or push it to the Docker Hub to share:
  - Build Dockerfile `docker build -t my-python-app .`
  - Run Dockerfile `docker run -p 5000:5000 my-python-app`

## Task: Run nginx web server in a Docker container

1. Open a Git Bash window (or terminal on Mac)

2. Download the latest nginx Docker image using a docker command

3. Run it so that it exposes it the running container on port 80 on your local machine

4. Run a Docker command to check if it’s running

5. Check it’s working by going to localhost or 127.0.0.1 in your web browser

6. Stop the container running

7. Well done, you’ve run the nginx web server in a Docker container on your local machine. Document everything you’ve learnt


## Task: Remove a container

1. Open a Git Bash window (or terminal on Mac)

2. Re-start the nginx container you were previously running

3. While the nginx container is running, try to remove the container – take note of the error

4. Work out the switch/option that you need to use so that you can forcibly remove a container which running

5. Run the docker command to check whether the container is still there

6. Well done, you’ve learnt to remove a container even if the container is already running. Document everything you’ve learnt


## Task: Modify our nginx default page in our running container

1. Re-run the nginx container exposed on port 80 of your local machine

2. Check the default webpage of the container in your web browser and keep it open for later

3. Access the shell of the nginx container that is running

4. If you get an error, about “TTY”, work out how to run an `alias` command to make sure that every time you run the docker command it will be prefixed with `winpty`

5. Once you’ve logged into the shell of the nginx container, do an update & upgrade

6. Try to run `sudo` - notice the problem, then install sudo to fix it

7. Check your present working directory, then navigate to where the default nginx file is kept

8. Use nano to edit index.html – notice the problem, then fix it so you can use nano

9. Once nano works, modify the HTML of the file so that instead of “Welcome to nginx!” the home page will be “Welcome to the Tech xxx Dreamteam!” – save your changes

10. Check how the default web page in the browser has changed

11. Well done, you’ve learnt to modify a running container by logging into it and changing a file. Document everything you’ve learnt


## Task: Run a different container on different port

1. Carrying on from the last task, you should already have running the nginx container that you modified

2. Try to run another container exposed on port 80 on your local machine (connect to port 80 inside the container) – here is the endpoint for the image to use: daraymonsta/nginx-257:dreamteam

3. Document the error and why it occurs

4. Remove the container we tried to run but couldn’t

5. Try to run the container from step 2 again but this time expose it on your local machine on port 90. Check this container is running in your web browser at `localhost:90`

---

<br>
<br>


# Day 1 Use Docker Hub to host custom images

## Task: Push host-custom-static-webpage container image to Docker Hub

1. Create an image from your running container which is running nginx with the index.html file we already modified earlier

2. Push the image to your Docker Hub account

3. Use a docker command to run the container which uses your pushed container image. The container image referenced should contain your username on Docker Hub.


## Task: Automate docker image creation using a Dockerfile

Rationale: We don't want to do the steps manually to change the default nginx page. We want to automate it.

1. Create a new folder such as techxxx-mod-nginx-dockerfile (not in a repo that will be published)

2. `cd` into the new folder

3. Create an index.html you'd like to use instead of the nginx default page

4. Create a Dockerfile to:

1. Use the nginx base image

2. Copy your index.html to the location of the nginx default page in the container

5. Use a docker build command to build your custom image

o Tag it similar to techxxx-nginx-auto:v1

6. Run the container

7. Push your custom image to Docker Hub

8. Use a docker command to run the container with uses your pushed custom image

9. Remove the local copy of your custom image

10. Re-run your container and force docker to pull the custom image from Docker Hub