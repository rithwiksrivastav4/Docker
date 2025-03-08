# Dockerfile

[Refer Here](https://docs.docker.com/reference/dockerfile/)  for official docs

* Dockerfile contains set of instructions required to build the image
* INSTRUCTION  args
  * examples

```bash
FROM nginx
FROM openjdk:17
RUN 
COPY . /app
```

___

* Each Instruction has a purpose
* Lets look at widely used instructions
  * FROM [Refer Here](https://docs.docker.com/reference/dockerfile/#from) for officials docs & FROM is used to choose the base image
  * LABEL: This is used to add the metadata
  * RUN: This instruction executes the commands written while building the image
  * EXPOSE: publishes the port information
  * ADD/COPY: They are used to copy the files into docker image
  * CMD: This will be executed as PID1 i.e. when we start the container this command executes and container will be in running state as long as the PID1 is running

___

## Shell form and Exec Form

* [Refer Here](https://docs.docker.com/reference/dockerfile/#shell-and-exec-form) for official docs
* Widely most of the Dockerfiles contains
* RUN in shell FORM
* CMD and Entrypoint in EXEC FORM

___

## Docker Image

* Docker Image should contain all the files necessary to run application
* Every Docker Image has a unique image id and name and tag
* Docker Image is collection of Readonly Layers
* A Layer is created during image creation by any instruction which leads to changes in the disk contents (RUN, ADD, COPY)
* Best Practice is to create few or less reusable layers

```bash
FROM azul/zulu-openjdk-alpine:17-jre
LABEL author=rithwik
ADD #add your url 
EXPOSE 8080
CMD ["java","-jar","/spc.jar"]
```
