# Docker
Docker is a way to isolate and run entire applications. With Docker it doesn’t matter if you are using a Mac, Windows, or Linux computer anymore. The entire development environment is isolated: programming language, software packages, databases, and more.

With Docker we now longer have to mess around with virtual environments. We can faithfully reproduce a production environment locally. And Docker can be shared among team members so everyone is working on the same setup. Wins all around.

## Linux Containers
### Docker is really just Linux containers which are a type of virtualization.

Virtualization has its roots at the beginning of computer science when large, expensive mainframe computers were the norm. How could multiple programmers use the same single machine? The answer was virtualization and specifically virtual machines which are complete copies of a computer system from the operating system on up.

An analogy we can use here is that of homes and apartments. Virtual Machines are like homes: stand-alone buildings with their own infrastructure including plumbing and heating, as well as a kitchen, bathrooms, bedrooms, and so on. Docker containers are like apartments: they share common infrastructure like plumbing and heating, but come in various sizes that match the exact needs of an owner.

## Containers vs Virtual Environments

Virtual environments are used to isolate Python software packages locally. We can create an isolated box for individual projects so one can use Python 2.7 and Django 1.5 while another can use Python 3.5 and Django 2.1 on the same computer. Virtual environments are great.

virtual environments can only isolate Python packages. They still rely on a global, system-level installation of Python albeit they can refer to the proper version. So when we use Python 2.7 in a project, we’re pointing to an installation of Python 2.7 on the computer itself, not actually within the virtual environment.

Also we can’t run a production database or other services within virtual environments so compared to Docker containers they are far more limited.

## to install Docker
we need to download the desktop app from this site https://www.docker.com/get-started/

then you have to install Docker Compose using `sudo pip install docker-compose`

then you should use `docker run hello-world` to check that every thing is installed correctly, it should give the screen below:

```

$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:9572f7cdcee8591948c2963463447a53466950b3fc15a247fcad1917ca215a2f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 ```
 ### another command to run is `docker info`, in the output foucs on the top lines :
 ```
 $ docker info
Containers: 1
 Running: 0
 Paused: 0
 Stopped: 1
Images: 1
```
## Images and Containers
An image is a snapshot in time of what a project contains. A container is a running instance of the image.

we use `Dockerfile` to create our own image and we use `docker-compose.yml` fils to run the containers .

A baking analogy we can use here is as follows:

- A Dockerfile is the recipe for a cake
- An image is a snapshot of the recipe at a given time
- A docker-compose.yml says how to make the cake
- And the container is the actual, baked cake

## Images
First create a local directory on your computer for our code, now define the image with `DockerFile` , Dockerfiles are read from top-to-bottom. The first instruction must be the FROM command which lets us import a base image to use for our image. This base image could be another Docker image or one we create entirely from scratch.

### Image Builds
to create the image for the first time use use the following command `docker image build .`

There will be a lot of output here ending with Successfully built and the hash id, b2c276538711, for the image, the actual has will changes .

use `docker image ls` to check existant images

### Image Layers
Every image is made up of one or more image layers. The base layer is often a flavor of Linux. 
image layering exists for two main reasons. First, each image layer is immutable–unchanged–like a git commit. This helps ensure consistency when two developers build the same image. The second reason is performance. Docker caches the steps in a `Dockerfile` to speed up subsequent builds.

## Containers
Now that we have our Python image how do we run it? Well just as a Dockerfile is a list of image instructions there is also a docker-compose.yml file that is a list of container instructions.

To demonstrate a real-world image and container example we will now “Dockerize” a basic Django web app.

Creat new Django project and run the server tomake sure that everything is working fine

Stop the local server with the command Control+c. And exit the virtual environment by also typing exit.





