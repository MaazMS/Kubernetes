### Namespace  
* Create virtual cluster inside k8s cluster is called namespace.  
* Namespaces are a way to divide cluster resources between multiple users.  
* if create any resource by default is store in default namespace.  
  
Q1. How to defined which resources support namespace?.     
`Example` node is not support because it is outside of cluster.  
`# kubectle api-resources | less `   
`# kubectle ap-resources | grep -i pod `   
  
 
### default namespace  
Kubernetes starts with four initial namespaces:  
```` 
NAME              STATUS   AGE
default           Active   1d
kube-node-lease   Active   1d
kube-public       Active   1d
kube-system       Active   1d 
```` 
**default namespace**   
1. The default namespace for objects with no other namespace.  
2. It is use when create resourced it support namespace and we do not give the namespace to that resources then it save  
to  default namespace.    
  
**kube-node-lease** 
It is  use for heartbeat. Also use to improves the performance of the node heartbeats.   
`Example` : The worker is send the heartbeat to master it is use to identify how many worker nodes is live and also master    
is assign the task to worker.   
**kube-public**   
In case that some resources should be visible publicly available without authentication.   
**kube-system**  
The namespace for objects created by the Kubernetes system.    