# Docker Survival Guide
 
### Get a public docker image
```
docker pull image 
```
Example: 
```
docker pull mysql 
```
 
### See what is running 
```
docker ps 
```

### Run a container 
```
docker run --name nameWeGiveIt -d -it -p 80:80 image 
```
-d: detached, as in server 

-it: interactive+tty. Without this commands like docker inspect won‘t be able to display anything to you. 

-p a:b Publish container port b as port a (or ip:port) on the host. 

Examples:
```
docker run --name mysql -d -it -p 8888:80 mysql
```
And to see this configuration:
```
docker container port mysql
```

### Run a container and override entrypoint
```
docker run -it --entrypoint sh image
```
This runs the interactive shell (sh) instead of the defined entrypoint.
 
### Run bash in a running container 
```
docker exec -it containerIdOrName /bin/bash 
```
...or if bash is not installed, the default shell:
```
docker exec -it containerIdOrName /bin/sh
```

### Copy file into container 
```
docker cp foo.txt mycontainer:/foo.txt 
docker cp mycontainer:/foo.txt foo.txt 
```
### Check container IP address 
```
docker inspect containerIdOrName  
```
 
### Stop container
```
docker stop container 
```
Container can be restarted, process is stopped, file system changes are preserved. 
### Start container
```
docker start containerIdOrName
```
Starts a previously stopped container. 
```
docker start -ai containerIdOrName
```
Starts a previously stopped container and attach interactive.

### Remove container
```
docker rm containerIdOrName
```
Stops and removes a container, file system and all. Image is preserved. 

### Pause container
```
docker pause containerIdOrName
```
Freezes all activity, only possible for Hyper-V containers. 
 
### Show containerIdOrName
docker inspect --format="{{.Id}}" containerIdOrName
 
### Access via powershell (Windows containers)
Enter-PSSession containerIdOrName -RunAsAdministrator 

### Build a container via Dockerfile and tag it
```
docker build -t myRepo/myContainer:myVersion .
```
