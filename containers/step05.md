# Simple App Containerization hands-on lab with Docker 
## Defining and running multi-container Docker applications using Docker compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a Compose file to configure your application’s services. Then, using a single command, you create and start all the services from your configuration.

Using Compose is basically a three-step process.
1. Define your app’s environment with a Dockerfile so it can be reproduced anywhere.
1. Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.
1. Lastly, run “docker-compose up” and Compose will start and run your entire app.

### In this exercise, we will create a python app that reads from a redis running in a different container.

Create a directory for the project:
```
mkdir composetest
cd composetest
```

Create a file called `app.py` in your project directory and paste this in:
```
from flask import Flask
from redis import Redis

app = Flask(__name__)
redis = Redis(host='redis', port=6379)

@app.route('/')
def hello():
    count = redis.incr('hits')
    return 'Hello World! I have been seen {} times.\n'.format(count)

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True)

```

Create another file called `requirements.txt` in your project directory and paste this in, to define the application’s dependencies:
```
flask
redis
```

Create a Dockerfile that builds a Docker image. The image contains all the dependencies the Python application requires, including Python itself. In your project directory, create a file named Dockerfile and paste the following:
```
FROM python:3.4-alpine
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

This tells Docker to:
1. Build an image starting with the Python 3.4 image.
1. Add the current directory . into the path /code in the image.
1. Set the working directory to /code.
1. Install the Python dependencies.
1. Set the default command for the container to python `app.py`

Define your services in a Compose file by creating a file called `docker-compose.yml` in your project directory and paste the following:
```
version: '2'
services:
  web:
    build: .
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: "redis:alpine"
```

This Compose file defines two services, web and redis. The web service:
1. Uses an image that’s built from the Dockerfile in the current directory.
1. Forwards the exposed port 5000 on the container to port 5000 on the host machine.
1. Mounts the project directory on the host to /code inside the container, allowing you to modify the code without having to rebuild the image.
1. The redis service uses a public Redis image pulled from the Docker Hub registry.

Build and run your app with Compose from your project directory. Start up your application using docker-compose up.
```
docker-compose up
```

You should see the following output
```
 Pulling image redis...
 Building web...
 Starting composetest_redis_1...
 Starting composetest_web_1...
 redis_1 | [8] 02 Jan 18:43:35.576 # Server started, Redis version 2.8.3
 web_1   |  * Running on http://0.0.0.0:5000/
 web_1   |  * Restarting with stat
```

Compose pulls a Redis image, builds an image for your code, and start the services you defined.

Enter `http://0.0.0.0:5000/` in a browser to see the application running.

If you’re using Docker on Linux natively, then the web app should now be listening on port 5000 # on your Docker daemon host. If `http://0.0.0.0:5000` doesn't resolve, you can also try  `http://localhost:5000`.

If you’re using Docker Machine on a Mac, use docker-machine ip MACHINE_VM to get the IP address of your Docker host. Then, open `http://MACHINE_VM_IP:5000` in a browser.

You should see a message in your browser saying:
```
Hello World! I have been seen 1 times.
```

Refresh the page and the number should increment.

Typing control-c will shutdown the containers.  If you started Compose with docker-compose up -d, you’ll probably want to stop your services once you’ve finished with them:
```
docker-compose stop
```


## Lab Navigation
1. [Lab Overview](./index.md)
1. [Installing Docker locally](./step01.md)
1. [Running a simple app in a Docker container locally](./step02.md)
1. [Lifecycle of a container](./step03.md)
1. [Creating and running Docker images using a Dockerfile](./step04.md)
1. [Defining and running multi-container Docker applications using Docker compose](./step05.md) *<-- You are here*
1. [Running CAT Sample App locally](./step06.md)

[Back to Index](../../index.md)
