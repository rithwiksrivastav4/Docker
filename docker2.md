# Port forwarding

![overview](E:\Docker\images\docker1.png)

* Let me create three applications in two containers each
  * nginx (it runs on port 80 )
  * jenkins (it runs on port 8080)
  * mysql container (it runs on port 3306)

## lets pull some images form docker

```bash
docker container run -d --name nginx1 nginx
docker container run -d --name nginx2 nginx
docker container run -d --name jenkins1 jenkins/jenkins
docker container run -d --name jenkins2 jenkins/jenkins
docker container run -d --name mysql1 -e MYSQL_ROOT_PASSWORD=password mysql:8.0
docker container run -d --name mysql2 -e MYSQL_ROOT_PASSWORD=password mysql:8.0
```

* To see the containers  

```bash
docker container ls
 or 
docker container ps
```
![preview](E:\Docker\images\docker2.png)

* The above containers are not userful for me as i cannot access them from outside the vm.
* Delete all the containers docker container rm -f $(docker container ls -q -a)
* Delete all the image docker image rm $(docker image ls -q)
* For port forwarding we have two modes
* static -p <hostport>:<containerPort>

![preview](E:\Docker\images\docker3.png)
![preview](E:\Docker\images\docker4.png)

* Dynamic -P
![preview](E:\Docker\images\docker5.png)

* Lets apply dynamic Port forwarding

```bash
docker container run -d -P --name nginx1 nginx
docker container run -d -P --name nginx2 nginx
docker container run -d -P --name jenkins1 jenkins/jenkins
docker container run -d -P --name jenkins2 jenkins/jenkins
docker container run -d -P --name mysql1 -e MYSQL_ROOT_PASSWORD=password mysql:8.0
docker container run -d -P --name mysql2 -e MYSQL_ROOT_PASSWORD=password mysql:8.0
```

![preview](E:\Docker\images\docker6.png)

* lets connect to jenkines

![preview](E:\Docker\images\docker7.png)

* lets connect to nginx 

![preview](E:\Docker\images\docker8.png)
