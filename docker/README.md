# Docker Environment

* Container -> The app
* Service -> How containers behave in production [Docker-compose!](https://github.com/docker/compose/releases)
* Stack -> Interactions of all the services

# Installation

For the installation of Docker on Debian, follow this link https://docs.docker.com/engine/installation/linux/docker-ce/debian/#install-from-a-package

## Docker Diagram
![Docker Diagram](https://www.docker.com/sites/default/files/Container%402x.png)

# Dockerfile
Dockerfile will define what goes on in the environment inside your container. Access to resources like networking interfaces and disk drives is virtualized inside this environment, which is isolated from the rest of your system, so you have to map ports to the outside world, and be specific about what files you want to “copy in” to that environment. However, after doing that, you can expect that the build of your app defined in this Dockerfile will behave exactly the same wherever it runs.

```
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

# Walkthrough Docker commands

This creates a Docker image, which we’re going to tag using -t so it has a friendly name.

`docker build -t friendlyhello .`

Run the app, mapping your machine’s port 4000 to the container’s EXPOSEd port 80 using -p.

`docker run -p 4000:80 friendlyhello`

Now let’s run the app in the background, in detached mode.

`docker run -d -p 4000:80 friendlyhello`

You get the long container ID for your app and then are kicked back to your terminal. Your container is running in the background. You can also see the abbreviated container ID with docker ps (and both work interchangeably when running commands):

`docker ps`

Now use docker stop to end the process, using the CONTAINER ID, like so:

`docker stop <CONTAINER ID>`

# List of the basic Docker commands

Here is a list of the basic Docker commands from Docker page

```
docker build -t friendlyname .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyname  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyname         # Same thing, but in detached mode
docker ps                                 # See a list of all running containers
docker stop <hash>                     # Gracefully stop the specified container
docker ps -a           # See a list of all containers, even the ones not running
docker kill <hash>                   # Force shutdown of the specified container
docker rm <hash>              # Remove the specified container from this machine
docker rm $(docker ps -a -q)           # Remove all containers from this machine
docker images -a                               # Show all images on this machine
docker rmi <imagename>            # Remove the specified image from this machine
docker rmi $(docker images -q)             # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```
