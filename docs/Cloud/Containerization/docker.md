# Docker
## What is Docker?
Docker is an open-source tool leveraging the technology of [containers](https://www.docker.com/resources/what-container) to easily package and deploy software applications. Docker can be used on a single computer to facilitate application development or on servers to easily deploy and maintain production-critical software.

Unlike "classic" virtualisation, where the entire system is virtualised, containers only bundle what is strictly necessary for the software to run (libraries, packages, ...). Low-level interactions are still handled by the host.

## Installation

Docker can be installed on a large number of platforms by following [the official documentation](https://docs.docker.com/get-docker/). 

Since Docker is mainly used on GNU/Linux systems, you'll find a simple script below to install docker on Debian-based distributions **in a lab environment**:

```bash
#!/bin/bash

# Upgrading the system and installing the necessary packages
sudo apt update && sudo apt upgrade --yes
sudo apt install --yes \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg \
     lsb-release

# Adding Docker GPG key
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Adding a docker.list file in the apt sources directory
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian bullseye stable' | sudo tee /etc/apt/sources.list.d/docker.list

# Installing docker and docker-compose
sudo apt update
sudo apt install --yes \
     docker-ce \
     docker-ce-cli \
     containerd.io \
     docker-compose

# Adding the current user to the docker group
# Allows the current user to use the docker commands without 'sudo'
sudo usermod -a -G docker $(whoami)
echo "You will need to logout for the group changes to take effect."

```


## Basic commands
Run a container:
```bash
docker run --name my_first_blog -p 7500:9000 -v my_first_blog_storage ghost
```
- `docker run` is the command to run a container. Execute `docker run --help` for more information.
- `--name my_first_blog` is the way we tell Docker to give a name (here "my_first_blog") to our container. If not specified, the container will be given a random name.
- `-p` (short for `--publish`) links a network port on the host (any of your choosing) to a port in the container (for ghost, it's 9000). In the above example, we make our blog available on port 7500.
- `-v` (short for `--volume`) tells Docker to create a volume (a "storage space") to store data from the container.
- `ghost` is the name of the image the container will be created and linked from.

List containers on the host:
```bash
docker ps -a
```

Start and stop containers:
```bash
docker start my_first_blog
docker stop my_first_blog
```

Remove containers:
```bash
docker rm my_first_blog
```

Manage Docker volumes:
```bash
docker volume
```

Manage Docker images:
```bash
docker image
```

## Build new images

A `Dockerfile` contains instructions on how to build images. New images are mostly built from other images, modified using instructions. Basically, each use of an instruction creates a new layer on top of the parent image. To optimize the storage and build speed, it is best to specify instructions that might modify the layer at the end of the `Dockerfile` (like the instruction to copy the application source code to the container).

Inside an empty directory (this directory will become the "build context"), create a file named `Dockerfile`, copy needed files for the build and eventually create a `.Dockerignore` file (same use as `.gitignore`).

Inside the `Dockerfile`, add instructions to create a new image. See the below examples taken from the official documentation:
```docker
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

The goal being to end up with the smallest image possible with the least amount of layers, it is possible to do "multi-stage builds". This way, the final image only contains the necessary programs and files:
```docker
FROM ubuntu:latest AS build
# Install the GCC compiler
RUN apt-get update
RUN apt-get install --yes gcc
WORKDIR /tmp/myprogram
# Copy the source file into our directory
COPY source.c .  
# Compiles the source into an executable
RUN gcc source.c -o source

FROM ubuntu:latest
# Copies the executable from the other image into the new one
COPY --from=build /tmp/myprogram/source /bin/source
# When the container starts, it executes the program
ENTRYPOINT ["/bin/source"]
```

Next inside the container, run the following command:
```bash
docker build .
```

### Instructions
See the official [Dockerfile reference](https://docs.docker.com/engine/reference/builder/).

|  Instruction  |Description | Example |
| ---- | ---------------------------------------- | ----- |
| `FROM`        | Specifies the image to build FROM, i.e. ubuntu or alpine. | `FROM alpine:3.13.6`
| `RUN`         | Runs a command necessary to install the application (creates a new layer) | `RUN ["wget", "-nv", "https://example.com/app.tar.gz"]`
| `CMD`         | Appends default arguments to `ENTRYPOINT`. If there is no `ENTRYPOINT` instruction in the Dockerfile, `CMD` can effectively specify a command to be run at the start of the container. | `CMD ["echo", "Hello World! "]` |
| `LABEL`       | Adds metadata (in a key/value pair) to the image, i.e. the author's name, the version, ... | `LABEL version="2.3"` | 
| `EXPOSE`      | Informs the Docker daemon which port(s) and protocol(s) the container listens on (ex: 80/udp) | `EXPOSE 443/tcp` |
| `ENV`         | Adds an environment variable to the container (KEY=value). Persisted in the final image. | `ENV ADMIN_PASSWORD="admin"` |
| `ADD` (**Obsolete**)  | Copies a local or external (from a URL) source to the image's filesystem. If the local file is compressed with a recognized algorithm (gzip, bzip2, xz), the ADD instruction decompresses it. It is best practice to replace this command with `RUN` instructions to avoid creating multiple layers. See the [official documentation](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy). | `ADD --chown=www-data:www-data ["./website_files",  "/var/www/html"]` | 
| `COPY`        | Copies the local file to the specified destination. `COPY` should be the instructions used instead of `ADD`. | `COPY --chown=www-data:www-data ["./website_files",  "/var/www/html"]` |
| `ENTRYPOINT`  | Command to be run at the start of the container. </br>For example, `ENTRYPOINT ["echo"]`, will execute the command `echo` at the start of the container (and the container will shut down). If nothing else is specified, it will print a blank line. </br>If `CMD` arguments have been added, it will print the content of `CMD`. </br>If the container was run with additional arguments like `docker run my_ubuntu_image One two three`, `CMD` will have no effect and the container will output "One two three". </br> Basically, `ENTRYPOINT` + `CMD` = default container command arguments ([see AWS blog post](https://aws.amazon.com/fr/blogs/opensource/demystifying-entrypoint-cmd-docker/)). | `ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]` |
| `VOLUME`      | Specifies a directory inside the container to become a volume or a mounting point on the host. Generally, it's best practice to create a volume if the container writes to it (log files, database data files, ...). If the container is run without specifying a volume, Docker creates an anonymous volume.| `VOLUME ["/var/lib/mysql"]`
| `USER`        | Specifies a user (previously created) to run any `RUN`, `CMD` or `ENTRYPOINT` instructions following.| `USER alice`
| `WORKDIR`     | Sets the "working directory" from which following instructions will be run. Creates the directory if it does not exist.</br> Note that at each instructions, a new shell is started. This makes `RUN cd` inconsequential on following instructions. | `WORKDIR /var/www/` |
| `ARG`         | Adds an environment variable to the container. Only used during build and not persisted in the final image. Useful to pass arguments to the `docker build` command. | `ARG USER=alice`
| `ONBUILD`     | Allows a child image (an image derived from the one currently being built) to execute instructions during build. See the [official documentation](https://docs.docker.com/engine/reference/builder/#onbuild). | `ONBUILD COPY $(APP_DIR) /var/www/`
| `STOPSIGNAL`  | Modifies the signal that is sent to stop the container. See the [official documentation](https://docs.docker.com/engine/reference/builder/#onbuild). | `STOPSIGNAL 9`
| `HEALTHCHECK` | Tells Docker how to check that the container is still working (even if the `ENTRYPOINT` process is still running), for example, by checking if it can still serve content. The command is executed from inside the container. | `HEALTHCHECK --interval=3m --timeout=3s CMD curl http://localhost || exit 1` | 
| `SHELL`       | Specifies the shell to be used to execute `RUN`, `CMD` or `ENTRYPOINTS` instructions. Default on Linux is `/bin/sh`, default on Windows is `cmd`.| `SHELL ["powershell"]`


## Storage

See the [official documentation about storage on Docker](https://docs.docker.com/storage/).

There is two ways to "detach" data from a container in Docker: bind mounts and volumes.

### Bind mounts
Bind mounts are binds between the host and the container. This type of storage is mostly used to link to configuration files from the host to the container. For example, the line `/home/user/web_files:/var/www` makes the `/home/user/web_files` path available to the container at `/var/www/`.

Since this is a **bind**, the container can modify or delete the files accessible to it. If, for example, the container deletes everything in `/var/`, the contents of '/home/user/web_files` will also get deleted.

### Volumes
Volumes are meant to abstract the external storage of the container from the host. It is thus simpler to move a volume from a host to an other without having to make sure the paths will stay de same.

The command to manage volumes is the following:
```bash
docker volumes --help
```


## Networks


## Compose


## Swarm