# container-app-workshop

Welcome to the Container App Workshop! This is an introductory workshop designed to help you get started with containers, how to connect them, how to build secure images, and how to control access to your application. This workshop is divided into several lessons, each focusing on a different aspect of containerization and its applications. The workshop is designed to be hands-on, so you will be able to follow along with the examples and exercises provided.

In the workshop, you will start with a simple container, and then we will advance to connecting containers, securing access to your application and then, use AI with Claude and MCP servers to build on your knowledge.

Each lab builds on the previous one, so it is best to complete them in order. The labs are designed to be completed in a few hours, but you can take your time and complete them at your own pace.

After completing all the labs in the workshop, you will have been introduced to several important concepts in containerization and how to build and deploy your applications. You will also have hands-on experience with the tools and technologies used in the workshop. You will be able to take these skills and apply them to your own projects and applications.

## Prerequisites

- Basic knowledge of system administration and networking
- Familiarity with the command line interface (CLI)

## Software Requirements

- Docker or Podman installed on your local machine (instructions are for Docker)
- A code editor (e.g., Visual Studio Code, Atom, etc.)
- A web browser (e.g., Chrome, Firefox, etc.)
- A terminal emulator (e.g., Command Prompt, PowerShell, Terminal, etc.)
- A GitHub account
- A Git client installed on your local machine (e.g., Git Bash, Git for Windows, etc.)
- Copilot or another AI assistant (optional until Lab 6)

installation instructions for Docker:
- [Docker Desktop for Windows](https://docs.docker.com/desktop/windows/install/)
- [Docker Desktop for Mac](https://docs.docker.com/desktop/mac/install/)
- [Docker Desktop for Linux](https://docs.docker.com/desktop/linux/install/)
- [Podman installation instructions](https://podman.io/getting-started/installation)

## Workshop Structure

### Part 1: Introduction to Containers
- [Lesson 1](lesson_1) is a simple introduction to containers and how to run a containerized application. You will learn how to create a Dockerfile, build an image, and run a container. 
- [Lesson 2](lesson_2) is an introduction to container orchestration and how to use Docker Compose to manage multiple containers. You will learn how to create a Docker Compose file, define services, and run the application using Docker Compose.
- [Lesson 3](lesson_3) is an introduction to how to test and troubleshoot networking in a containerized environment.You will learn how to test connectivity between containers using `ping`, `nc`, and `wget` using a `busybox` test container. access the application running in one container from another container. You will then test the configuration works by accessing the application from your web browser.
---
### Part 2: Securing Access to Your Application
- Lab 4 is an introduction to Cloudflare tunnels running in a container and connecting it to our nginx container created in the previous lab. You will learn how to create a Cloudflare tunnel, configure it to connect to the nginx container, and access the application from the internet.
- Lab 5 is an introduction to authentication and authorization using OIDC. You will learn how to use OIDC to authenticate users and authorize access to the application running in the container. You will also learn how to use a reverse proxy to secure the application and control access to it.
- Lab 6 is an introduction to minimal containers and how to use them to reduce the attack surface of your application. You will learn how to create a minimal container image using Chainguard images and how to scan for vulnerabilities in the image.
---
### Part 3: Building and Deploying Your Application
- Lab 7 is an introduction to using GitHub Actions to automate the build and deployment of your containerized application. You will learn how to create a GitHub Actions workflow, build the image, and deploy it to a container registry.
- Lab 8 is an introduction to using Claude and MCP servers to build and deploy your application. 

