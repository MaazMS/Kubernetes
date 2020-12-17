### why we need services  
* Imagine that you have been asked to deploy web app  
Q1. How does this front end web app is exposed to outside the world?.   
Q2. How does this back end web app is connected backend database ?.   
Q3. How do we resolve pod ip change, when it die ?.  

### services    
* Services is a way of grouping of pods that are running on cluster.  
* services are cheap and you can have as many services as possible within cluster.  
* imagine that we have created pods and services but how these services discover their respective pod and connect to it.  
ans is label. Example service are front-end and back-end and the pod label are define front-end and back-end then services   
are recognized their respective pods.  

### Types of services 
1. ClusterIP    
2. NodePort   
3. LoadBalancer    
**ClusterIP**
1. This default type service.   
2. It exposes cluster-internal IP.   
3. You can reach the service only from within the cluster.     
`Example`  connect front-end to back-end   
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/Cluster%20Ip.png?raw=true)   
**NodePort**  
1.  This type of service exposes the service outside the world.    
2. How to communicate services inside of cluster to outside of world.     
Example web app connect to internet.  

Q1. Why we need node port?.  
1. Webapp inside the pod when pod is die controller create new pod with new ip.   
2. Their is no connectivity between user and pod.     
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/Node%20Port.png?raw=true)   
**Explain**  
1. User is connect with node port.  
2. Node port is connect the pod inside of cluster.   
3. There for node port is use to communicate between pod inside of cluster and user is connect to node port.  
**Note**   
1.Define node port in range 30000  to 32767 define in manifest file.    
2. If not define k8s define dynamically in range between 30000  to 32767.    
3. Outside of that range define node port is not node port.  
**LoadBalancer**   
1. when the app instance is distribute across couple of node on cluster.   
2. multiple pod in single node and multiple pods in multiple nodes the LoadBalancer is use.       
Q1. Which ip is use to access the app?.      
Q2. Do not overload the specific node and leave the other node ideal?.     
Q3. which ip provide to end user?.  
Q4. Are these comfortable to end user?.   
Q5. How traffic balance equally?.    
1. If use LoadBalancer it will create automatically load balancer in the backend and generate public ip.  
2. It is forward all the traffic.    
3. It is costly.

### Type of port   
1. Node port  
2. Port   
3. Target port   
**Node port**  
It is port where pod is running, to  use this port along with node ip to access the app outside the world.   
**Port**   
Service it self.  
**Target port**  
1. Actual port where app is running. 
2. Typically port and target port number is same.    
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/Type%20pf%20port.png?raw=true)   