# Simple App Containerization hands-on lab with Docker 
## Creating and Running Docker images using a Dockerfile 

Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using “docker build” users can create an automated build that executes several command-line instructions in succession.

In the following steps, you will create a docker file, to use in building an image and then run the new image on your local machine

### First step is to create a new directory to include all you need to build the image.
On MacOS
```
mkdir mydockerbuild; cd mydockerbuild
```

On Windows
```
c:\md mydockerbuild
c:\cd mydockerbuild
```

### Now, you are ready to create a new text file named Dockerfile to include details about your image. For example, copy and paste the following Dockerfile to your directory.
```
FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay
```

For this exercise, we used the docker/whalesay:latest image, which is based on Ubuntu Liunx distribution. 

The RUN statement will execute the command and record changes to the file system.  It will NOT record the state of processes or start daemons.

The CMD statement defines the default command to execute when the container is created. This command runs fortune -a and sends its output to the cowsay command.

### Now, you are ready to build an image from your docker file. The -t parameter gives your image a tag, so you can run it more easily later. Don’t forget the . command, which tells the docker build command to look in the current directory for a file called Dockerfile.
```
docker build -t docker-whale . 
```
 
### You can now check that you have this new image on your local machine using docker images
```
docker images
```

The output should look something like this
```
REPOSITORY           TAG          IMAGE ID          CREATED             SIZE
docker-whale         latest       c2c3152907b5      4 minutes ago       275.1 MB
docker/whalesay      latest       fb434121fc77      4 hours ago         247 MB
hello-world          latest       91c95931e552      5 weeks ago         910 B
```
 
### Now, you are ready to run your new docker image using docker run
```
docker run docker-whale
```

The output should look something like this
```
 --------------------------------------
< You will be successful in your work. >
 --------------------------------------
                    ##        .
              ## ## ##       ==
           ## ## ## ##      ===
       /""""""""""""""""___/ ===
  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
       \______ o          __/
        \    \        __/
          \____\______/

```


## Lab Navigation
1. [Lab Overview](./index.md)
1. [Installing Docker locally](./step01.md)
1. [Running a simple app in a Docker container locally](./step02.md)
1. [Lifecycle of a container](./step03.md)
1. [Creating and running Docker images using a Dockerfile](./step04.md) *<-- You are here*
1. [Defining and running multi-container Docker applications using Docker compose](./step05.md)
1. [Running CAT Sample App locally](./step06.md)

[Back to Index](../../index.md)
