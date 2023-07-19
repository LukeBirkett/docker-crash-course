# Notes on Docker Crash Course
Video Course by TechWorld with Nana [[Video Link](https://www.youtube.com/watch?v=pg19Z8LL06w)]

## What is Docker?
- Makes developing and deloying applications easier
- Packages an applications into a container
- The container holds everything the application needs to run, i.e. code, libraries, dependancies, run-time and environment configuration
- Application + running environment packaged in a container
- The container can easily be shared and distributed
- Without this, i.e. before docker, the person running the app (or every dev on the team) would need to install and configure everything needed on their local machine
- Big issue here is when users have different OS systems making the installation of dependacies different 
- Docker allows you to standardize this process by just running a pre-configured docker container

## Docker Desktop
- This installs the Docker engine, GUI and CLI tool.

## What Are Images?
- An immutable template and defines how a container will be realized
- An excetubable application artifact
- It holds source code but also environment configurations
- You can also execute commands in order to create virtual enviroments, create directories, files etc

## What is a Container?
- A running instances of an Image
- There can be mutliple containers run from a single image

## What is the Docker Registry?
- A place to store and distribute docker images
- Includes offical images from applications such as postgres, mongo, python etc
- DockerHub is the registry hosted by Docker itself which is also the biggest

## Registry vs Repository
- Registry = a service providing storage for repositories
- Repository = A collection of related images with the same name but different versions

## Image Versioning
- Docker images are versioned and can be identified by their tag

## How to get and use image?
- This is known as pulling an image
- Pull image = `docker pull {name}:{tag}`
- Docker by default searched for the image on DockerHub
- Start container = `docker run {name}:{tag}`
- Running a container will take over the terminal so run a container in the background you run it in detached mode = `docker run -d {name}:{tag}`
- To check the logs of a running container = `docker logs {container_name}`
- You can skip the `pull` step of the process and go straight to `run`. If the image is not availble locally Docker will download it and perform the build
- `docker stop container`
- Container ID's and name can be used interchangably but a name is easier to remember
- To set a container name as run use `docker run --name {container_name} -d name:tag`

## Docker Stop
- Each time a container is run it will create a new one
- `docker stop container_name`
- `docker ps -a` shows all containers includes those that has stopped
- A container can be restart `docker start container_name`

## Port Binding
- Running a container as above will open it in an isolated port, do we able to access it on our local machine we need to map it to a port on our local host
- `docker run -d -p {host_port}:{container_port} {name}:{tag}`
- Standard practice is to use the same host and container port number

## Bulding Own Docker Images
- Create using files called a Dockerfile
- Dockerfiles start from a base image, for example python

## DockerFile commands
- `FROM` build image from this base image
- `RUN` executes commend in shell within container enviroment
- `COPY` copies folders or files from local machine into container `COPY local_file /container_location/`
- `WORKDIR` changes working directory the same way as `cd` would
- `CMD` similar to run in the same that is executes commands but this is intended to be the last thing run in the Dockerfile and should be things that related to the running of the application within the container. There can only be one `CMD` in a Dockerfile whereas there can be mutliple of the other commands
```
FROM scratch
ADD hello /
CMD ["/hello"]
```

## Building an Image
- `docker build {-t or --tag} name:tag dockerfile_location`
- Each instruction in the Dockerfile creates a layer. These layers can be see in the build logs
- After running the image will now show up with `docker images`
- Which you can now run using `docker run`

## Docker CLI
- `docker images` list of images
- `docker ps` list of containers running
