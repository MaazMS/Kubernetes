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
**ClusterIP**
1. This default type service.   
2. It exposes cluster-internal IP.   
3. You can reach the service only from within the cluster.   
`Example`  connect front-end to back-end 
**NodePort**  
