# Docker 🐳
**Table of Content**
- [Pull Images & Spin Containers](#pull-images--spin-containers)
	- [Pull A Docker Image](#pull-a-docker-image)
	- [Run A Docker Container](#run-a-docker-container)
- [List Stuff](#list-stuff)
	- [List local Docker Images](#list-local-docker-images)
	- [List local Containers](#list-local-containers)
- [Control Existing Docker-stuff](#control-existing-docker-stuff)
	- [Start an existing Container](#start-an-existing-container)
	- [Stop a Container](#-stop-a-container)
	- [Execute Something in an existing Container](#execute-something-in-an-existing-container)
	- [Display Logs of a Container](#display-logs-of-a-container)
	- [Inspect Containers / Images](#inspect-containers--images)
- [Remove Stuff](#remove-stuff)
	- [Remove Containers](#remove-containers)
	- [Remove a Docker Image](#remove-a-docker-image)

---

## Pull Images & Spin Containers

### Pull A Docker Image
```bash
docker pull <IMAGE NAME>[:<TAG>]
```
here,
- `<TAG>` is used to specify the version.


### Run A Docker Container
```bash
docker run [-i] [-t] [-d] [-p <H>:<C>] [--name <NAME>] <IMAGE NAME> <COMMAND>
```
here,
- NOTE : if the specified image is not available locally, docker will automatically grab it from dockerhub
- `-i` flag is used to run the container in interactive mode.
- `-t` flag is to open TTY session.
- `-d` flag is to run the container in detach mode (Run container in background)
- `[-p <H>:<C>]` flag is for Port Forwarding from Container’s Port `<C>` to Host’s port `<H>`
- `[--name <NAME>]` flag is for adding a custom name to the container.
- `<COMMAND>` can be an actual command for the container to run. if `-d` flag is not used then, output from the container will be displayed. After the execution of the command ended, the container will stop

---

## List Stuff

### List local Docker Images
```bash
docker images
```

### List local Containers
There are two commands for the same task.

**Command 1 :**
```bash
docker container ls [-a]
```

**Command 2 :**
```bash
docker ps [-a]
```
here,
- `-a` command is used to list all running containers + stopped containers

---

## Control Existing Docker-stuff

### Start an existing Container
```bash
docker start <CONTAINER ID> 
```
here,
- `<CONTAINER ID>` can be fetched by `docker ps` command.

### Stop a Container

**Command 1 : For Multiple Containers**
```bash
docker kill <CONTAINER ID> [<CONTAINER ID1> <CONTAINER ID2> ...]
```

**Command 2 :**
```bash
docker stop <CONTAINER ID>
```
here,
- `<CONTAINER ID>` can be fetched by `docker ps` command.

### Execute Something in an existing Container
There are two commands for the same task.

**Command 1 :**
```bash
docker exec [-i] [-t] [-d] <CONTAINER ID> <COMMAND>
```

**Command 2 :**
```bash
docker container exec [-i] [-t] [-d] <CONTAINER ID> <COMMAND>
```
here,
- `-i` flag is used to run the container in interactive mode.
- `-t` flag is for TTY.
- `-d` flag is to run the container in detach mode (Run container in background)
- `<CONTAINER ID>` can be fetched by `docker ps` command.
- `<COMMAND>` can be an actual command for the container to run, or Commend shell can be fetched by `docker ps` command.  If `-d` flag is not used then, output from the container will be displayed.

### Display Logs of a Container
```bash
docker logs [--since <time>] <CONTAINER ID> 
```
here,
- `<CONTAINER ID>` can be fetched by `docker ps` command.
- `[--since <time>]` is used to show logs since the given time.

### Inspect Containers / Images
```bash
docker inspect <IMAGE ID/CONTAINER ID>
```

## Remove Stuff

### Remove Containers

**Command 1 :**
```bash
docker rm <CONTAINER ID>
```

**Command 2 : To remove all containers**
```bash
docker container prune [-f]
```
here,
- `<CONTAINER ID>` can be fetched by `docker ps` command.
- `-f` = Force.

### Remove a Docker Image
```bash
docker rmi <IMAGE NAME> [-f]
```
here,
- `-f` = Force.
- NOTE : if the container of an image is running, then the image can’t be removed
