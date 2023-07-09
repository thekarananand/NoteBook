# Dockerfile

| Keyword                  | Action                             |
|--------------------------|------------------------------------|
| `FROM <Image>`           | Selecting the base image           |
| `RUN <Bash Command>`     | Run a bash command (as root user)  |
| `COPY <Source> <Target>` | Copies files into container        |
| `ENTRYPOINT <Command>`   | Command to run at start Container  |
| `EXPOSE <Port>`          | To Expose the port                 |

## Building
``` bash
docker build <Dockerfile> -t <ImageName>
```
- `<ImageName>` is generally `<UserName>/<AppName>`

---

### Docker Build Command

``` bash
docker build <parent dir of dockerfile> -t <imgName> [ -t <imgName2> ... ]
```

- `<imgName>` is generally, `<userName>/<appName>:<tag>`

### Docker login

``` bash
docker login
```

### Docker Push 

``` bash
docker push <imgName>
```

In the case of
- Error storing credentials
- pass not initialized
- password store is empty

try

``` bash
rm -rf ~/.password-store/docker-credential-helpers
gpg --generate-key
pass init <generated gpg-id public key>
```

---


## Dockerfile : CMD vs ENTRYPOINT

### CMD
Runs the specified command on startup of the container. But, when a command is specified with `docker run` or `docker exec`, this command gets overwritten.

Syntax :
``` dockerfile
CMD sleep 5
```
or
``` dockerfile
CMD [ "sleep", "5" ]
```
> in the second syntax, first thing should be a command/executable

### ENTRYPOINT
Runs the specified command on startup of the container. But, It appends anything specified in `docker run` or `docker exec` to the ENTRYPOINT command. So, it's useable for taking arguments form users.

Syntax :

``` dockerfile
ENTRYPOINT [ "sleep" ]
```

While running :
``` bash
docker run <image> 5
```
> in above syntax, first thing should be a command/executable

now, final command at start up = `sleep 5`

### To set a default value in ENTRYPOINT

``` dockerfile
ENTRYPOINT [ "sleep" ]
CMD [ "5" ]
```

- On, `docker run <image>`, the startup command = `sleep 5`
- But on, `docker run <image> 10`, the startup command = `sleep 10`
