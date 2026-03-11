# Cloud Infrastructure and Virtualisation CA

## Overview

This document provides a comprehensive guide to Docker in virtual environments. In this document, I will create a virtual machine (VM) on Microsoft Azure and install Docker on it. It covers containerisation fundamentals, practical Docker workflows, and Docker Compose for multi-container orchestration. By the end, you'll understand how to containerise applications, manage Docker images and containers, and deploy multi-service applications using Docker Compose.

## What is Docker?

Docker is a container platform used to build, ship, and run applications in isolated environments called containers.

- **Container:** A lightweight package that includes your app + its dependencies.
- **Image**: A read-only template used to create containers.
- **Why use it:** It makes apps run consistently across different machines (developer laptop, test server, cloud VM).
In short, Docker helps avoid “works on my machine” issues by standardizing runtime environments.

## Getting Started

1. Setup an account on Microsof Azure
2. Create a Virtual Machine that has Ubuntu
3. Start your Virtual Machine


Before installing Docker Engine, first add and configure Docker's official APT repository.

To do this, run the following commands in your VM terminal, as shown in the image below:

![alt text](images/docker-apt-ss.png)

## Containerise an Application

-
