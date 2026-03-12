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

## Installing Docker Engine on your Ubuntu Virtual Machine

Before installing Docker Engine, first add and configure Docker's official APT repository.

To do this, run the following commands in your VM terminal, as shown in the image below:

![alt text](images/docker-apt-ss.png)

Once you have installed the APT repository, run the following command to install the Docker packages:

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Finally, after installing the packages, run the following command to start the hello-world image:

```bash
sudo docker run hello-world
```

 If the image below is shown, everything was installed correctly:

![alt text](images/docker-hello-world.png)

## 1. Containerise an Application

Before you can run the application, you need to have the project source code on your virtual machine. Fork the repository from the Docker getting-started tutorial source code:

[https://github.com/docker/getting-started-app](https://github.com/docker/getting-started-app)

Once the source code is available in your GitHub repository, clone it to your virtual machine, as shown in the image below:

![alt text](images/git-clone.png)

## Building the App Image

To build the image, you need a Dockerfile. A Dockerfile is an extensionless file that contains a set of instructions Docker uses to build an image. 

```bash
FROM node:24-alpine
WORKDIR /app
COPY . .
RUN npm install --omit=dev
CMD ["node", "src/index.js"]
EXPOSE 3000
```

The Dockerfile should be saved in the root directory of your application, and it must be named Dockerfile with no file extension.

After that, inside your application folder, build the image by using the following command:

```bash
docker build -t getting-started .
```

The image bellow shows the image being created in the virtual machine: 

![alt text](images/docker-image-creation.png)

After building the image, you can verify that it was created successfully by running the following command:

```bash
docker image ls
```

## Start App Container

Now that the image has been created, you can use the following command to run the application in a container:

```bash
docker run -d -p 127.0.0.1:3000:3000 getting-started
```

If your application is running, it should appear in the list of running containers when you run `docker ps`, as shown in the image below:

![alt text](images/docker-containers-running.png)

## 2. Update the Application

In this section, you will learn how to update the application and image.

On the **line 56** of the file ```src/static/js/app.js``` located in your github getting-started repo, make the following change:

 ```<p className="text-center">You have no todo items yet! Add one above!</p>```

## Stopping and Removing a Container

Once you have updated the code, **stop and remove** the old container so you can rebuild the image with your changes.

To do it, run the following command:

```bash
docker rm -f $ID_CONTAINER
```

Now, you just need to rebuild your image using ```docker build``` and run the container again to see that the change was made, as it shows the image bellow:

![alt text](images/updated-code.png)

## 3. Share the Application

To share your application, follow the steps below:

1. Have an account on Docker Hub.
2. Select the **Create Repository** button.
3. Give **getting-started** as the name of the repo and **leave the visibility as Public**, as in the image below:

![alt text](images/creating-repository-dockerhub.png)

## Push the image

In order to push the image to Docker Hub follow the steps below:

1. Login to your Docker Hub by using the command ```docker login -u $YOUR_USERNAME```, as in the image below:

![alt text](images/login-docker-hub.png)

2. Run the `docker tag` command to assign a new name to the `getting-started` image, replacing `YOUR-USER-NAME` with your Docker Hub username:

```bash
docker tag getting-started YOUR-USER-NAME/getting-started
```

3. Finally, run `docker push YOUR-USER-NAME/getting-started` to push the image to your Docker Hub repository, as it shows in the image bellow

![alt-text](images/dockerhub-push.png)



