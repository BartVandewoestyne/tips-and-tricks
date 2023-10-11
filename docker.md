# Testing your Docker installation:
```
$ docker run hello-world
```

# Image vs container

* A container is a running environment for an image.
  A container also has a port which is binded to, which allows
  you to talk to the application running inside it.
  Has virtual file system.

* Everything in docker hub are 'images'.
  Images have tags or versions (see e.g. Docker hub)

# Main Docker commands

## docker pull

To pull images (e.g. from DockerHub):
```
$ docker pull mongo:4.2
```
which is shorthand for
```
$ docker pull docker.io/library/mongo:4.2
```

## docker run

To run an image.  This starts the image in a container in an attached mode.
With CTRL+C it is stopped.

With the `-d`, the container runs in detached mode:
```
$ docker run -d redis
```
You only get the id of the container, but it is still running.

To both pull an image (with potentially a specific version) and start a container:
```
$ docker run redis:4.0
```

To start containers with binding between host and container ports, e.g. to bind my laptop's port 6000 to the container's port 6378:
```
$ docker run -p6000:6378 redis
```

To create a container with a certain name instead of an automatically generated name:
```
$ docker run -d -p6001:6379 --name redis-older redis:4.0
```

## docker start and stop

To restart a container (e.g. if application crashed or error happened).
Take first part of docker id and do
```
$ docker stop 8381867e8242
```

To restart it again:
```
$ docker start 8381867e8242
```

Note the difference between `docker run` and `docker start`.  `docker start` works with containers.  After you created the container with `docker run`.  `docker start` is to restart a stopped container.

## docker ps

To list running containers
```
$ docker ps
```

`PORTS` specifies on which ports the container is listening for incoming requests.
Two containers can actually listen on the same portnumber.  The host where the containers are running on must then have different bindings.  E.g.
```
host port 3000 -> container port 3000
host port 3001 -> container port 3000
```
To list both running and stopped containers:
```
$ docker ps -a
```

# Debugging containers

## docker logs

To see the logs that a certain container is producing:
```
$ docker logs 51cdac3132f6
```
or use the name of the container (see `docker ps` output in the right):
```
$ docker logs some_name
```
(containers get random names, but you can name them too...)

## docker exec -it

To get the terminal of a running container!  E.g. to navigate to a directory inside that container, check logfile, check configuration file, print out environment variables,...
```
$ docker exec -it cae903a74202 /bin/bash
$ docker exec -it cae903a74202 /bin/sh
```
The `-it` stands for `interactive terminal`.  You can also use the name instead of the ID.  One of `bash` or `sh` should work (always).

Just do `exit` to go out.

Often, containers are based on lightweight linux distro's, so you don't always have commands at hand.

# Other commands:

Checking all existing images on my laptop (e.g. to cleanup stale images):
```
$ docker images
```

To delete an image from this list:
```
$ docker rmi 2e0a4d16e074
```

To delete a Docker container:
```
$ docker rm 3c58e681c8c5
```

# docker network

Docker creates its own isolated network (on the host) where the containers are running in.  Two containers in same Docker network can talk to each other using just the container name.

Applications that run outisde of Docker, are going to connect using localhost:27017.  Later, whe package our application in its own image, we can put it in its own docker container in that same network, and its going to connect.  Browser is then going to connect using localhost:3000

docker by default provides some networks:
```
$ docker network ls
```

to create network:
```
$ docker network create mongo-network
```

After you created the network, to run containers in this network, you have to provide the network option when you run the container in the `docker run` command.
```
# start mongodb
$ docker run -d \
    -p 27017:27017 \
    -e MONG_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    --net mongo-network \
    --name mongodb \
    mongo

# start mongo-express
$ docker run -d \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
    -e ME_CONFIG_MONGODB_SERVER=mongodb \
    --net mongo-network \
    --name mongo-express \
    mongo-express
```
With the above, mongo-express should be able to connect to mongodb.

To remove all unused networks:
```
docker network prune

```

# Docker Compose

Tool to make running multiple containers.

docker-compose files are files where you can write all the docker-run commands for all your containers in a structured way.
```
version:'3'       # version of docker-compose
services:
  mongodb:        # container name (--name option)
    image: mongo  # the image that you specified in your docker-run command (can include version tag)
    ports:
     -27017:27017 # ports HOST:CONTAINER
    environment:
     - MONGO_INITDB_ROOT_USERNAME=admin
     - MONGO_INITDB_ROOT_PASSWORD=password
  mongo-express:
    image: mongo-express
    ports:
     - 8080:8080
    environment:
     - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
     - ME_CONFIG_MONGODB_ADMINPASSWORD=password
     - ME_CONFIG_MONGODB_SERVER=mongodb
```
Indentation is important!
Network is not needed.  Docker Compose takes care of creating a common Network!

How to start the containers using this file?
```
$ docker-compose -f mongo.yaml up
```
Interesting things:
* A network is created with the containers in it.
* Logs of both containers are shown mixed.

How to stop the containers?
```
$ docker-compose -f mongo.yaml down
```
This shuts all containers and removes the network.

# Dockerfile

To build your own Docker *image* to deploy your application.

```
FROM node   # from what image is this one based? node is another image (see dockerhub)

ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password       # Better to do itin docker compose so that you don't have to rebuild the image in case of changes

RUN mkdir -p /home/app   # execute any Linux command to the container environment, not the host. directory is created *inside* of container, not on my laptop

COPY . /home/app  # copy command that executes on the HOST machine!

CMD ["node", "server.js"]  # execute an entrypoint Linux command inside the container
```
Difference between `RUN` and `CMD`: CMD is an 'entrypoint command'.  You can have multiple RUN commands, but CMD is just one.  This marks for Dockerfile that this is the command that you want to execute as an entry point.

To build an image using a Dockerfile:
```
docker build -t my-app:1.0 .
```

Note that whenever you adjust the Dockerfile, you MUST rebuild the image!

# Private Docker Registry 

Options:
 * AWS: Amazon ECR
 * Nexus
 * Digital Ocean

## AWS

Create private repository for Docker (a Docker Registry)
aws.amazon.com
 => make account
  ECR (Elastic Container Registry)
=> In AWS, one repository per image!!!  For each iamge, you have its own repository.
   But in that repo you store different tags of the same image.
1. first login to the private repo using `docker login`:
     $(aws ecr get-login --no-include-email --region eu-central-1)
   Make sure you have AWC Cli installed and Credentials configured
2. build your image
     docker build -t my-app .
3. tag your image
     docker tag my-app:latest 664574038682.dkr.ecr.eu-central-1.amazonaws/my-app:latest
     (`docker tag` renames the image)
4. Push your image to the newly created AWS repo:
     docker push 664574038682.dkr.ecr.eu-central-1.amazonaws/my-app:latest

# Docker Volumes

There is no data persistence in containers!  Everything that you configured or stored, is gone!  E.g. databases or stateful applications.
Docker Volumes allows you to have persistence.

Volumes plug the physical filesystem in the container filesystem (mounting).
When container writes to its filesystem, it gets written on the host (and vice versa).

3 types of volumes:
  1. Host Volumes
       docker run -v /home/mount/data:/var/lib/mysql/data
                     host dir <-> container dir
  2. Anonymous Volumes:
       docker run -v /var/lib/mysql/data
       (you do not specify a dir on the host, that is taken care of
        by docker itself in /var/lib/docker/volumes/random-hash/_data)
  3. Named Volumes (Improvement of Anonymous volumes)
       docker run -v name:/var/lib/mysql/data
     You can reference the volume by name

=> most used and should be using is the Named Volumes (because there
   are benefits by letting docker actually manage those volume
   directories on the host)

With docker-compose, you can also define volumes.

``` 
version: '3'

services:

    mongodb:

        image: mongo

        ports:
         - 27017:27017

        volumes:
         - db-data:/var/lib/mysql/data

    mongo-express:

        image: mongo-express

        ...

volumes:
    db-data
```
You can actually mount one and the same reference to a volume on the host to more than one container.  That is beneficial if the containers need to share the data.

To see where docker volumes are located (depends on Windows/Linux)
Windows: C:\ProgramData\docker\volumes
Linux and Mac: /var/lib/docker/volumes

# Other useful commands

## docker inspect

To see low-level information on Docker objects:
```
docker inspect <container-id>
```

# References:

* Docker Tutorial for Beginners [FULL COURSE in 3 Hours]:
  https://youtu.be/3c-iBn73dDE?si=b93UrrspGp2mDcWl
