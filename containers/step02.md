# Simple App Containerization hands-on lab with Docker 
## Running a Simple App in a Container locally

### Open a command-line terminal, and run some Docker commands to verify that Docker is working as expected. 

Check the latest version of docker is installed using:
```
docker version
```

Run docker ps and docker run hello-world to ensure the daemon is working as expected
```
docker ps
```

### Now, you can run a simple hello-world container using “docker run.” This command will:
1. check to see if you had the hello-world software image
1. downloaded the image from the Docker Hub
1. loaded the image into the container and "ran" it

```
docker run hello-world
```

### Now, we will run a simple webserver on your local machine using the nginx docker image. 

Run a simple webserver in a container on your local machine
```
docker run -d -p 80:80 --name webserver nginx
```

In a web browser, go to `http://localhost/` to bring up the home page. 

Run docker ps while your web server is running to see details on the webserver container.
```
docker ps 
```

The output should look something like this
```
    CONTAINER ID        IMAGE                COMMAND                  CREATED              STATUS              PORTS                         NAMES
    56f433965490        nginx                "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   webserver
```

If you want to stop the webserver, type: docker stop webserver and start it again with docker start webserver
```
docker stop webserver
docker start webserver
```

To stop and remove the running container with a single command, type: docker rm -f webserver.
```
docker rm -f webserver
```

## Lab Navigation
1. [Lab Overview](./index.md)
1. [Installing Docker locally](./step01.md)
1. [Running a simple app in a Docker container locally](./step02.md) *<-- You are here*
1. [Lifecycle of a container](./step03.md)
1. [Creating and running Docker images using a Dockerfile](./step04.md)
1. [Defining and running multi-container Docker applications using Docker compose](./step05.md)
1. [Running CAT Sample App locally](./step06.md)

[Back to Index](../../index.md)
