# Docker
Problem to solve: Some programs work on a system but doesn't work on another system

Software development Life Cycle: Design -> Development -> Deployment -> Testing/release

Docker is present in the entire workflow. But its main use is in the deployment.

# How it works

Define dependencies and requirements in `Dockerfile`. This file can be used to create docker images. In the `ìmage` you'll have all the application, requirements and dependencies. When you run docker image you get `docker container`. The docker container are the runtime instance of the docker image. The docker image can be store also in the Docker Hub. 

In the docker hub, you can pull images to create containers in any environment. So you can create a docker container on a test envirnoment or on a stage envirnoment.

Docker has a client-server architecture. The command interface is the client and send commands to the server (docker) in form of commands line interface (CLI) or REST API's request and runs this on the Docker Engine.

# Benefits of Docker

You can test a docker in a container wich simulates the production envirnoment.

# Play With Docker

If you would like to use Docker and try some commands, this is a good [application](https://labs.play-with-docker.com/)

# Docker Image
See commands for images
```
docker images --help
```
Show images in your mac
``` 
docker images
```
Pull an image with the latest tag
```
docker pull <image name>
```
Pull with a particular tag
```
docker pull <image name:tag>
```