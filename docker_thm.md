## Basic Syntax docker:
The syntax for Docker can be categorized into four main groups:
- Running a container
- Managing & Inspecting containers
- Managing Docker images
- Docker daemon stats and information
## Docker Pull Command:
*Docker pull command is use for downloading an docker image from the internet*
`docker pull nginx`
	***(image:tag)
 `docker pull ubuntu` 
 `docker pull ubuntu:latest`
 `docker pull ubuntu:22.04`
 `docker pull ubuntu:20.04`

## Docker Image:
The `docker image` command, with the appropriate option, allows us to manage the images on our local system. To list the available options, we can simply do `docker image` to see what we can do. I’ve done this for you in the terminal below
***verify Images:
`docker image ls`
Remove Images
`docker image rm`
`docker image rm ubuntu:22.04`

## Running Your First Container:
`docker run [OPTIONS] IMAGE_NAME [COMMAND] [ARGUMENTS...]`
the options enclosed in brackets are not required for a container to run.
***Example:***
docker run -it[interact] ubuntu /bin bash 

***Information about Container*** `docker ps`

## Running Containers...Continued:
`docker run -d helloworld`
This argument tells the container to start in "detached" mode. This means that the container will run in the background.

`docker run -it helloworld`
This argument has two parts. The "i" means run interactively, and "t" tells Docker to run a shell within the container. We would use this option if we wish to interact with the container directly once it runs.

`docker run -v /host/os/directory:/container/directory helloworld`
This argument is short for "Volume" and tells Docker to mount a directory or file from the host operating system to a location within the container. The location these files get stored is defined in the Docker file.

`docker run -p 80:80 webserver`
This argument tells Docker to bind a port on the host operating system to a port that is being exposed in the container. You would use this instruction if you are running an application or service (such as a web server) in the container and wish to access the application/service by navigating to the IP address.

`docker run --name helloworld`
This argument tells Docker to remove the container once the container finishes running whatever it has been instructed to do.

## Docker Files:
`INSTRUCTION argument`
******
***FROM ubuntu***
This instruction sets a build stage for the container as well as setting the base image (operating system). All Dockerfiles must start with this.

******
***RUN whami***
This instruction will execute commands in the container within a new layer.
******
***COPY /home/cmnatic/myfolder/app/***
This instruction copies files from the local system to the working directory in the container (the syntax is similar to the `cp` command).
******
***WORKDIR /  (sets to the root of the filesystem in the container)***
This instruction sets the working directory of the container. (similar to using `cd` on Linux).

******
***CMD /bin/sh -c script.sh***
This instruction determines what command is run when the container starts (you would use this to start a service or application).

******
***EXPOSE 80***
This instruction is used to tell the person who runs the container what port they should publish when running the container

## Building First Container:
we have a Dockerfile, we can create an image using the `docker build` command. This command requires a few pieces of information:

1. Whether or not you want to name the image yourself (we will use the `-t` (tag) argument).
2. The name that you are going to give the image.
3. The location of the Dockerfile you wish to build with.

I’ll provide the scenario and then explain the relevant command. Let’s say we want to build an image - let’s fill in the two required pieces of information listed above:

1. We are going to name it ourselves, so we are going to use the `-t` argument.
2. We want to name the image.
3. The Dockerfile is located in our current working directory (`.`).

## Leveling up Our Dockerfile:
1. Use Ubuntu 22.04 as the base operating system for the container.
2. Install the “apache2” web server.
3. Add some networking. As this is a web server, we will need to be able to connect to the container over the network somehow. I will achieve this by using the `EXPOSE` instruction and telling the container to expose port _80_.
4. Tell the container to start the “apache2” service at startup. Containers do not have service managers like `systemd` (this is by design - it is bad practice to run multiple applications in the same container. For example, this container is for the apache2 web server - and the apache2 web server only).

## Docker Compose:
|             |                                                                                                                         |                        |
| ----------- | ----------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| **Command** | **Explanation**                                                                                                         | **Example**            |
| up          | This command will (re)create/build and start the containers specified in the compose file.                              | `docker-compose up`    |
| start       | This command will start (but requires the containers already being built) the containers specified in the compose file. | `docker-compose start` |
| down        | This command will stop and **delete** the containers specified in the compose file.                                     | `docker-compose down`  |
| stop        | This command will stop (**not** delete) the containers specified in the compose file.                                   | `docker-compose stop`  |
| build       | This command will build (but will not start) the containers specified in the compose file.                              | `docker-compose build` |