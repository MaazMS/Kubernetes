# Pods  
![](https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)   
Q1. What is pod ?. 
1. A pod is the smallest execution unit in Kubernetes.     
2. It contain one or more containers and volume.  
3. if a pod fails Kubernetes can automatically create a new replica of that pod to continue operations.  
4. Pods contain shared networking and storage resources for their containers.  
5. Pods are automatically assigned unique IP addresses.
6. Pod containers share the same network namespace, including IP address and network ports.    
7. Pods run on nodes in your cluster.  
You can consider a Pod to be a self-contained, isolated "logical host" that contains the systemic needs of the application it serves.  

# Pod lifecycle  
1. Pods are ephemeral.  
2. They are not designed to run forever, and when a Pod is terminated it cannot be brought back  
3. In general, Pods do not disappear until they are deleted by a user or by a controller.      
4. Pods do not "heal" or repair themselves. for example node fail and pod delete for any reason it does not replace itself.    
5. Each Pod has a PodStatus API object, which is represented by a Pod's status field.   
6. Pods publish their phase(summary of the Pod in its current state.) to the status: phase field.   
7. phase of pods are Pending, Running, Succeeded, Failed, Unknown,   
`Pending` : Pod has been created and accepted by the cluster, but containers inside of pod are not yet running.  
 This phase includes scheduled on a node and downloading images.   
`Running` : Pod has been bound to a node, and all of the containers have been created. At least one container is running.  
`Succeeded` : All containers in the Pod have terminated successfully. Terminated Pods do not restart.  
`Failed`: At least one container has failure in pod.  
`Unknown` : The state of the Pod cannot be determined.   

