### Master node
* Master is responsible to managing whole cluster.  
* It monitors the health check of these nods   
* It showing information about the member of cluster.  
* its configuration member of cluster inside the master.  
* When worker nodes fail it move workload from fail node to another healthy worker node.   
* It is responsible for `scheduling`, ` provision`, `controlling `and `exposing`    


Four primary components of master.    
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
1. Node control manager   
2. Replication controller    
3. Endpoint controller    
4. Services account and token controller    
* These controllers are responsible  for the overall health of the entire cluster.     

**4. etcd**  
* It is a distributed key-value lightweight database.     
* It is developed by core os.   
* It is a central database.     
* Store current status of cluster at any point of time.   

![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/master.png?raw=true)  


 
 
   


 
   
