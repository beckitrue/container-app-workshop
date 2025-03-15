# README

In this lab, we will learn how to configure `nginx` as a reverse proxy.

This is one part of a series of labs on building systems with containers. We will build on this learning in subsequent labs.

## Introduction

Why have a reverse proxy? A reverse proxy is a server that sits between clients and backend servers. It forwards client requests to the appropriate backend server. A reverse proxy can perform various tasks such as load balancing, authentication, SSL termination, and caching. 

In this lab, we will use `nginx` as a reverse proxy to serve static files and a simple web application with Flask.


## Objectives

- Configure `nginx` as a reverse proxy
- Use `nginx` to serve static files
- Use `nginx` to server a simple web application with Flask


## Learning Outcomes

- Understand the concept of a reverse proxy
- Understand how to configure `nginx` as a reverse proxy
- Understand how to bind mount a volume to a container so that we can make configuration changes on our host machine and not in the container

## Prerequisites

- Basic knowledge of Docker
- Basic knowledge of `nginx`
- Basic knowledge of Flask
- Basic knowledge of web servers and web applications

You will need to have Docker installed on your machine. If you do not have Docker installed, you can download it [here](https://www.docker.com/products/docker-desktop).

You will need a text editor to edit files. You can use any text editor of your choice. If you do not have a text editor installed, you can download Visual Studio Code [here](https://code.visualstudio.com/).

## Instructions

### Step 1: 
Clone this [container-app-workshop repo](https://github.com/beckitrue/container-app-workshop) to your local machine if you have not done so already.


### Step 2:
Begin with creating the Flask application container by following the instructions in the `simple-web` directory

### Step 3: 
Create the `nginx` container by followig the instructions in the `nginx` directory
