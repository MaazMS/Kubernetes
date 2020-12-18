### kubernetes control plane
1. API server   
2. Etcd    
3. scheduler  
4. controller manager   
5. Cloud controller manager   

**1. API server** 
* Gatekeeper for the entire cluster.  
* operation perform such as Create, update,delete.     
* API server validate and configure api objects such as replication, controller and deployment.     
* To interact with api server using tool cubectl, also called cube control and cube cuddle.  

**2. Scheduler**  
* It is used for scheduling pods across multiple nodes.    
* To write an artifact and pass an api  server and it passes to the scheduler it will look for appropriate nodes that    
meet the requirement and schedule pods on that node.       

**3.Control Manager**  
1. Node control manager : Eg. If node is not responding then restart node.  
2. Replication controller : Eg. It ensures that the number of pods are up and running at any given pint of time.     
3. Endpoint controller : Eg. Creating new endpoints such as  joining services.   
4. Services account and token controller : Eg. creating new user account and new access  token.   
* These controllers are responsible  for the overall health of the entire cluster.     

**4. etcd**  
* It is a distributed key-value lightweight database.     
* It is developed by core os.   
* It is a central database.     
* Store current status of cluster at any point of time.  

**5.Cloud controller manager**   
Kubernetes is not control host infrastructure then Cloud controller manager come into picture.      
1. Node Controller: Eg. It is responsible for node inside the cluster.     
2. Router Controller: Eg. It is responsible for routing inside the cluster with outside the world.     
3. Service Controller: Eg. It is responsible for provide the services.       
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/kubernetes%20control%20plane.png?raw=true)  