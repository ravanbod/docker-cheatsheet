# Docker Cheat Sheet
In this repository, I give some examples of docker commands.
# Pulling images
You can pull images with `docker pull <repository>:<tag>` 

`docker pull mysql:8`

`docker pull nginx:latest`

# Inspecting and gathering data from images
You can inspect an image with `docker inspect <repository>:<tag>`

`docker inspect mysql:8`

# Save an image
you can save an image to as a .tar file using `docker image save -o <output-file> <repository>:<tag>`

`docker image save -o nginx.tar nginx:latest`

# Load an image
You can load an image using `docker image load`

`docker image load < nginx.tar`

or

`docker image load -i nginx.tar`

# Import an image
You can import an image using `docker image import <file-path> <repository>:<tag>`

`docker image import nginx.tar nginx:latest`

# Running a container (basic)

You can run a container using `docker run <repository>:<tag>`

You can read manual of this command using `docker run --help`

# Running a container named `nginx` and mapping ports
`docker run -d --name nginx -p 8081:80 nginx`

It will map 8081 of host to 80 of container.

note: `-d` detaches a container

# Display the running processes of a container
`docker top <container-id or container-name>`

`docker top nginx`

`docker top db65c23ca7accf470646d42c096e86f061771bed934a7c2c0ff03f0586f66430`

# Removing dangling images
Dangling images are images which have `REPOSITORY` but `TAG`
```
REPOSITORY                        TAG               IMAGE ID       CREATED        SIZE
alpine                            <none>            e9adb5357e84   2 days ago     5.57MB
```
You can remove dangling images using `docker image prune`