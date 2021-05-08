# Build Image

## Hands-on

### Build the Docker Image from the [`Dockerfile`](./Dockerfile)

```bash
docker build -t my-image .

  # [+] Building 161.8s (11/11) FINISHED
  #  => [internal] load build definition from Dockerfile                                        0.0s
  #  => => transferring dockerfile: 607B                                                        0.0s
  #  => [internal] load .dockerignore                                                           0.0s
  #  => => transferring context: 34B                                                            0.0s
  #  => [internal] load metadata for docker.io/library/centos:7                                 2.9s
  #  => [auth] library/centos:pull token for registry-1.docker.io                               0.0s
  #  => [internal] load build context                                                           0.0s
  #  => => transferring context: 684B                                                           0.0s
  #  => CACHED [1/5] FROM docker.io/library/centos:7@sha256:0f4ec88e21daf75124b8a9e5ca03c37a5e  0.0s
  #  => => resolve docker.io/library/centos:7@sha256:0f4ec88e21daf75124b8a9e5ca03c37a5e937e0e1  0.0s
  #  => [2/5] RUN  yum clean all   && yum repolist   && yum -y update   && sed -i "s/en_US/a  100.3s
  #  => [3/5] RUN  yum -y install tar unzip vi vim telnet net-tools curl openssl   && yum -y   56.0s
  #  => [4/5] COPY . .                                                                          0.1s
  #  => [5/5] RUN sed -i "s/@_WHERE_@/CentOS 7 Container/g" local-to-container.txt              0.4s
  #  => exporting to image                                                                      1.9s
  #  => => exporting layers                                                                     1.9s
  #  => => writing image sha256:fa60503416f29520fb4e5f7133211a743cd243785a1745b382c87367cfbe6b  0.0s
  #  => => naming to docker.io/library/my-image                                                 0.0s
```

### Check the Image in the Local Docker Image List

```bash
docker image ls my-image

  # REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
  # my-image     latest    6a0132b4596f   12 seconds ago  204MB
```

### Run a Container from the Docker Image

```bash
docker run -ti --name my-container my-image

  # [root@************ /]# exit
```

- Detach from container: type `Ctrl + P Q`

### Execute command at the Container

```bash
docker exec -ti my-container cat local-to-container.txt

  # Hello! We meet in 'CentOS 7 Container'!
```

### Attach to the Container

```bash
docker attach my-container

  # [root@bc5dd8098e51 /]# exit
  # exit
```

### Check in list the Container

```bash
docker container ls

  # CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
  # (Nothing...)

docker container ls -a

  # CONTAINER ID   IMAGE      COMMAND       CREATED         STATUS             PORTS       NAMES
  # bc5dd8098e51   my-image   "/bin/bash"   1 minutes ago   Exited 5 seconds               my-container
```

### Start the Stopped Container

```bash
docker start my-container

  # my-container

docker container ls

  # CONTAINER ID   IMAGE      COMMAND       CREATED         STATUS         PORTS     NAMES
  # bc5dd8098e51   my-image   "/bin/bash"   2 minutes ago   Up 2 seconds             my-container
```

### Stop the Running Container

```bash
docker stop my-container

  # my-container
```

### Remove the Stopped Container

```bash
docker rm my-container

  # my-container
```

### Remove the Docker Image

```bash
docker rmi my-image

  # (Like this..)
  # Untagged: my-image:latest
  # Deleted: sha256:fa60503416f29520fb4e5f7133211a743cd243785a1745b382c87367cfbe6b22
  
docker image ls

  # REPOSITORY   TAG    IMAGE ID       CREATED        SIZE
  # centos       7      8652b9f0cb4c   5 months ago   204MB
```

- If you want to delete base image(`centos:7`), try below command

  ```bash
  docker rmi centos:7
  ```
