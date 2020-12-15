### Namespace  
* Create virtual cluster inside k8s cluster is called namespace.  
* Namespaces are a way to divide cluster resources between multiple users.  
* if create any resource by default is store in default namespace.  

 
### default namespace  
Kubernetes starts with four initial namespaces:  
```` 
NAME              STATUS   AGE
default           Active   1d
kube-node-lease   Active   1d
kube-public       Active   1d
kube-system       Active   1d 
```` 
`default` The default namespace for objects with no other namespace.  
It is use when create resourced it support namespace and we do not give the namespace to that resources then it save to  
**default namespace**   
`kube-node-lease` : 
`kube-public ` :  in case that some resources should be visible publicly available without authentication.   

`kube-system  ` The namespace for objects created by the Kubernetes system.    
Q1. How to defined whcih resources support namespace  
1. node is not support because it is ouside of cluster.  
`# kubectle api-resources | less `   
`# kubectle ap-resources | grep -i pod `   `  
