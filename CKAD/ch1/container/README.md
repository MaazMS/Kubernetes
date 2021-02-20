### 
k8s is all about container.   
## What is container?   
1. A container is self-contained ready to run application.   
1. Inside container every thing that need to run application.    
1. Container itself process running on host os.       
1. Container have all on board that is required to start the application.   
1. The container runtime is running on a host platform and establish communication between local host kernel  
and container.  
1. So all containers no matter what they do, run on top of the same local host kernel.     
1. kernel in host os deliver to access the hardware.  
1. Container on host os all on same kernel.  
1. In order to work container use container runtime.  
1. Container is use container runtime.   
1. On top of container runtime have multiple container with isolated environment.  
1. Isolated environment using namespace.   

1. Noet It is not possible to run windows container on top of linux container.  


### Namespace feature  
1. Provide isolated environment.  
1. Network   
1. file  
1. Users  
1. Processes  
1. IPCs (Inter Process  Communication )  

## Network  
1. Every container have it's own network.   
## file    
1. Container is like chroot environment.  
## Users  
1. Container have it's own user.  
## Processes  
1. COnatiner only see it's own process.               
## IPCs (Inter Process  Communication )      

## linux Cgroup   
1. It offers resource allocation and limitation.  


