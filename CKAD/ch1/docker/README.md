## Understanding Docker  
1. Docker is important in the container landscape, but docker is not the only way to run container.  
1. When it started in 2013, docker is offered the following.  
1. Container image format.  
1. Dockerfile which is a method for building container image.   
1. A way to manage container images.  
1. A way to run containers.      
1. A way to manage container instances.  
1. A solution to share container images.  
Note: For k8s perpective no matter whcih container runtime you use.   

## busybox  
1. It is image   
1. It minimal linux os image.   
1. It is use to run something.      

## Docker comand  
1. docker ps  
1. docker ps -a   
1. docker start  
1. docker stop  
1. docker restart   
1. docker kill   (terminate container)
1. docker rm    (remove container)

## inspect  specific setting.  
1. docker ps  
1. docker inspect <id> | less 
1. docker inspect --format=`{{.NetrworkSettings.IPAddress}}` container name    
1. docker inspect --format=`{{.State.Pid}}` container name   

## Understanding Container Logging  

1. Logs by default are written to the container
1. Use docker run -rm -v/dev/log:/dev/log/fedora:latest logger "message from container" to capture container logs in    
   the host operating system.  
1. Type journalctl | grep container to see this test log message on the container host.   
