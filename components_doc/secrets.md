### why we need secrets  
1. Deploy the container app in k8s, the app how same sensitive data such as name and password.    
2. The sensitive data is not store as text in mainfest file.  
3. How to manage secrets in k8s?.   

### secrets  
1. It is k8s object to handle small amount of sensitive data. such as password, token , key.  
2. Reduces risk of exposing sensitive data while deploying pod.  
### where secrets key  
1. When deploy pod ink8s cluster, pull the images and run container assume that their is some custom config  
that are done by over side based over requirement.   
2. When custom config have some sensitive data then secrets come.  
3. secrets create outside of pods and container.  
4. secrets have no clue to which pods and container is use.  
5. It deploy nay pods, container and any number of time.  
6. secrets are store inside of ETCD database on k8s master.  
7. There is the limit and size of secrets. max size of secrets not more then 1MB.  

### How to inject secrets in pods  
1. Volumes(mount)  
2. Env variable(expose) 

* Sent only to the target nodes (not available for all nodes )   
   
  
