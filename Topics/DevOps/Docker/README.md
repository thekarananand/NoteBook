# Docker

### Pulling an image from DOCKER HUB
```bash
docker pull <IMAGE NAME>[:<TAG>]
```
here,
- `<TAG>` is used to specify the version.


### Creating a container from an Image
```bash
docker run [-i] [-t] [-d] [-p <H>:<C>] [--name <NAME>] <IMAGE NAME> <COMMAND>
```
here,
- NOTE : if the specified image is not available locally, docker will automatically grab it from dockerhub
- `-i` flag is used to run the container in interactive mode. This allow to give inputs in `stdin`. Otherwise no `stdin` 
- `-t` flag is to open TTY session.
- `-d` flag is to run the container in detach mode (Run container in background)
- `[-p <H>:<C>]` flag is for Port Forwarding from Container’s Port `<C>` to Host’s port `<H>`
- `[--name <NAME>]` flag is for adding a custom name to the container.
- `<COMMAND>` can be an actual command for the container to run. if `-d` flag is not used then, output from the container will be displayed. After the execution of the command ended, the container will stop

### List all local Docker Images
```bash
docker images
```

### List running Containers
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
- `-a` flag is to list all (running + stopped) containers.

### Execute Something in an existing Container
There are two commands for the same task.

**Command 1 :**
```bash
docker exec [-i] [-t] [-d] <CONTAINER NAME/ID> <COMMAND>
```

**Command 2 :**
```bash
docker container exec [-i] [-t] [-d] <CONTAINER NAME/ID> <COMMAND>
```
here,
- `-i` flag is used to run the container in interactive mode.
- `-t` flag is for TTY.
- `-d` flag is to run the container in detach mode (Run container in background)
- `<COMMAND>` can be used to assign a task to the container. If `-d` flag is not used then, output from the container will be displayed. After the completion of the assigned task, the container will stop.

### Just Start an existing Container
```bash
docker start <CONTAINER NAME/ID> 
```

### How to attach to a container running in Detach Mode?
``` bash
docker attach <CONTAINER ID/NAME>
```
### Stop a Container

**Command 1 :**
```bash
docker kill <CONTAINER ID> [<CONTAINER ID1> <CONTAINER ID2> ...]
```

**Command 2 :**
```bash
docker stop <CONTAINER ID>
```

### Remove a Container
```bash
docker rm <CONTAINER ID>
```
here,
- `<CONTAINER ID>` can be fetched by `docker ps` command.

### Display Logs of a Container
```bash
docker logs [--since <time>] <CONTAINER ID> 
```
here,
- `<CONTAINER ID>` can be fetched by `docker ps` command.
- `[--since <time>]` is used to show logs since the given time.

### Remove all stopped containers
```bash
docker container prune [-f]
```
here,
- `-f` = Force.

### Remove a Docker Image
```bash
docker rmi <IMAGE NAME> [-f]
```
here,
- `-f` = Force.
- NOTE : if the container of an image is running, then the image can’t be removed

### Create a new image from a Container
```bash
docker commit [-m "<message>"] <CONTAINER ID> <NEW IMAGE NAME[:<TAG>]>
```
here,
- `-m "<message>"` flag is used to attach a message

### Inspect Containers / Images
```bash
docker inspect <IMAGE ID/CONTAINER ID>
```