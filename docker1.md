# Docker Installation

* For Guided creation of ec2 instance watch classroom recording
* Docker installation

* Simplest installation

```bash
curl -fsSL https://get.docker.com -o install-docker.sh
sh install-docker.sh
```

* NOw add the current user to  docker group

```bash
sudo usermod -aG docker $USER
sudo usermod -aG docker ubuntu
```

## When we install docker the following components will be installed

* docker ce (docker daemon)
* docker ce cli (docker client)
* containerd
* docker compose
* docker buildx
* Docker Package based installation

------------------------------------------------------

### Docker Images

Docker images have tags which represent versions. If you don’t pass tag, docker will assume it to be latest

```bash
docker pull nginx
```

------------------------------------------------------


### Docker images from docker hub

* official images <application>:<tag>
* community images organization/application:tag
* private images <username>/application:tag

------------------------------------------------------


## Docker container creation modes

* Attached/Foreground

```bash
docker container run --name nginx1 nginx
```

* Detached

```bash
docker container run -d --name nginx1 nginx
```

* interactive termninal: you want to get into shell while creating container

```bash
docker container run -it --name nginx1 nginx /bin/bash
```

------------------------------------------------------


## Execution in running contianers

* Docker has a command called as exec

```bash
docker container exec nginx whoami
```

* We can use exec to run a command inside container
* we can also use exec in an interactive way

```bash
docker container exec -it nginx2 /bin/bash
```

------------------------------------------------------

## Observations:

* Inside containers, the PID 1 is the application startup
* Container will have its own process tree
* Contianer will have its own network, diskmounts, CPU and RAM allocated
* Restrictions can be placed on RAM and CPU
* Inside containers we have its own set of users