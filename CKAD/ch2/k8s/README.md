## What is Kubernetes?

1. Kubernetes is "an open-source system for automating deployment, scaling and managing of containerized applications"         
(https://kubernetes.io)   
2. The word Kubernetes comes from Greek, and means "pilot of the ship"   

## Kubernetes Origins
1. Kubernetes is based on Google Borg, the internal system that Google has been using for many years to offer 
   access to its applications.
https://al.google/research/pubs/pub43438             
2. Borg was also the origin of important Linux kernel features, used in containers nowadays, such as namespaces  
3. Google donated the Borg specification to the Cloud Native Computing Foundation (CNCF) which was the start of Kubernetes   
    
## Working with Kubernetes    
1. The kubectl command line utility provides convenient administrator access, allowing you to run many tasks against the cluster
2. Direct API access using commands, such as curl, allows developers to address the cluster using API calls from custom scripts  
3. The Kubernetes Dashboard can be installed to run on the Kubernetes master node.  

## The Role of the Kubernetes API

1. An Application Programmers Interface (API) is the interface between a client and a server.  
2. An API is used to standardize how to access items provided by the server.  
3. The Kubernetes API defines objects in a Kubernetes environment.  
4. Any command that is used in a Kubernetes environment, is working in some way with the API.  
5. Also, all that can be done in Kubernetes, can be explained by exploring API features.   
