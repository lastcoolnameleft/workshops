# Simple App Containerization hands-on lab with Docker 
## Running CAT Sample App locally

Now you are ready to run the CAT sample app on your local machine. This sample app is a ASP.NET app which you will also use on Azure with the Orchestrator in the second portion of the lab. This code material are available [here](https://github.com/dave-read/container-service-dotnet-continuous-integration-multi-container). 

### Clone the repo from github into a new local directory on your machine using: 
```
mkdir ASPNETAPP
cd ASPNETAPP  
git clone https://github.com/dave-read/container-service-dotnet-continuous-integration-multi-container 
cd container-service-dotnet-continuous-integration-multi-container
```

### Now, compile the ASP .NET Core application code. This uses a container to isolate build dependencies that is also used by VSTS for continuous integration:
```
docker-compose -f docker-compose.ci.build.yml run ci-build
```
> On Windows, you currently need to pass the -d flag to docker-compose run and poll the container to determine when it has completed

> Note: if you get an error about not being able to access a shared folder, open the Docker for Windows settings from the system tray, and in the Shared Drives tab, ensure that the drive where your lab files are stored is checked (enabled).

```
docker-compose -f docker-compose.ci.build.yml run –d ci-build
```

### Now build Docker images and run the services:
```
docker-compose up --build
```

The frontend service (service-a) will be available at `http://localhost:8080`.


## Lab Navigation
1. [Lab Overview](./index.md)
1. [Installing Docker locally](./step01.md)
1. [Running a simple app in a Docker container locally](./step02.md)
1. [Lifecycle of a container](./step03.md)
1. [Creating and running Docker images using a Dockerfile](./step04.md)
1. [Defining and running multi-container Docker applications using Docker compose](./step05.md)
1. [Running CAT Sample App locally](./step06.md) *<-- You are here*

[Back to Index](../../index.md)
