# Docker Cheat Sheet
In this repository, I give some examples of docker commands.
# Pulling images
You can pull images with `docker pull <repository>:<tag>` .

`docker pull mysql:8`

`docker pull nginx:latest`

# Inspecting and gathering data from images
You can inspect an image with `docker inspect <repository>:<tag>`.

`docker inspect mysql:8`

# Save an image
you can save an image to as a .tar file using `docker image save -o <output-file> <repository>:<tag>`.

`docker image save -o nginx.tar nginx:latest`

# Load an image
You can load an image using `docker image load`.

`docker image load < nginx.tar`

or

`docker image load -i nginx.tar`

# Import an image
You can import an image using `docker image import <file-path> <repository>:<tag>`.

`docker image import nginx.tar nginx:latest`

# Running a container (basic)

You can run a container using `docker run <repository>:<tag>`.

You can read manual of this command using `docker run --help`.

# Running a container named `nginx` and mapping ports
`docker run -d --name nginx -p 8081:80 nginx`

It will map 8081 of host to 80 of container.

note: `-d` detaches a container.

# Display the running processes of a container
`docker top <container-id or container-name>`

`docker top nginx`

`docker top db65c23ca7accf470646d42c096e86f061771bed934a7c2c0ff03f0586f66430`

# Removing dangling images
Dangling images are images which have `REPOSITORY` but `TAG`.
```
REPOSITORY                        TAG               IMAGE ID       CREATED        SIZE
alpine                            <none>            e9adb5357e84   2 days ago     5.57MB
```
You can remove dangling images using `docker image prune`.

# Kill a container
You can kill a container using `docker kill <container-id or name>`.

`docker kill db65c23ca7accf470646d42c096e86f061771bed934a7c2c0ff03f0586f66430`

`docker kill nginx`

# Installing nginx on a alpine container

```
~ » docker run -it alpine sh                                                            
/ # apk add nginx
fetch https://dl-cdn.alpinelinux.org/alpine/v3.15/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.15/community/x86_64/APKINDEX.tar.gz
(1/2) Installing pcre (8.45-r1)
(2/2) Installing nginx (1.20.2-r0)
Executing nginx-1.20.2-r0.pre-install
Executing nginx-1.20.2-r0.post-install
Executing busybox-1.34.1-r4.trigger
OK: 7 MiB in 16 packages
```

# Pausing a container

You can pause a container using `docker pause <container-id or name>`.

`docker pause db65c23ca7accf470646d42c096e86f061771bed934a7c2c0ff03f0586f66430`

`docker pause nginx`

# Redirect container-id of a container to a file
`docker run -d redis > myredis.cid`

# Limit a container
`docker run -d --cpus 1.5 --memory=512m --memory-swap=512m --cpuset-cpus=0,2 nginx`

# Setting environment variables

`docker run --rm -it -e NAME=behrad -e CLASS=dws alpine sh`

After that, you can verify this setting using `env` command in container.

```
~ » docker run -it -e NAME=behrad -e CLASS=dws alpine sh                               
/ # env
CLASS=dws
HOSTNAME=d458fcfc5a64
SHLVL=1
HOME=/root
NAME=behrad
TERM=xterm
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
PWD=/
```

# Mounting a host directory to a container and changing the working directory
You can mount a volume using `-v or --volume` and `-w or --workdir` to change working directory.

`docker run -v $PWD/test:/data -w /data alpine`

It will mount `$PWD/test` of host to `/data` of container.

# Dockerfile

Just an example ...

```
ARG VERSION=latest
FROM alpine:$VERSION
ENV CLASS=dws

RUN apk add nginx

EXPOSE 80/tcp

VOLUME /data

ADD . /data
COPY . /data

ENTRYPOINT ["nginx", "-s" , "start"]
```

[@dwsclass](https://github.com/dwsclass) dws-ops-005-docker

[@dwsclass](https://github.com/dwsclass) dws-ops-006-docker

[@dwsclass](https://github.com/dwsclass) dws-ops-007-docker
