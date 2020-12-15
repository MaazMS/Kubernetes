# Pods  
![](https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)   
### pod
1. A pod is the smallest execution unit in Kubernetes.  
`Example `   
In the virtualization world, a virtual machine is an atomic unit and in docker world “container” is an atomic unit and In the Kubernetes world, Pods are the atomic units.     
2. It contain one or more containers and volume.    
### pod deployment  
step 1 : write manifest file inside the mainfest file container images.  
step 2 : mainfest file submit to API-SERVER on master node.   
step 3 : master node decide deploy pod on appropriate worker nodes in k8s.  
* Generally our aim is deploy application in the form of container but k8s not deploy container directly on workers nods.    
* k8s is encapsulate container inside the `pod`  
Q1. How scale up application?.  
a. Add new container with same pod the ans is wrong.  
b. we create new pod with same application instance in that nod.  
Q2. What happened when the nod does not have sufficient space?.  
a. create new vm and join that new nod to cluster once it ready k8s deploy pod on new nod.   
Q3. How scale down application?.  
1. delete the pod the application is scale down.  

```gitignore
Kubernetes manifests are used to create, modify and delete Kubernetes resources such as pods, deployments, services or   
ingresses. It is very common to define manifests in form of . yaml files and send them to the Kubernetes API Server via   
commands such as kubectl apply -f my-file. yaml or kubectl delete -f my-file.
```   

### Multi- container  
![](https://matthewpalmer.net/kubernetes-app-developer/articles/networking-overview.png)  

1. one pod for one container. which is explain above.  
2. Multi container communicate with each other directly because by referencing localhost, share same network, storage, namespace.  
 
Q1. What case we use multiple container in one single pod?.   
1. Some times we need helper container for some support task for main container that time we use multiple container.  

Q2. What type of support task we do for helper container?.   
1. processing user enter data.  
2. processing files which is uploaded by user.  

Q3. what time we create or delete helper container?.   
1. When new app container is created helper container also created.  
2. When app container die helper container is also die.  

### pod Networking  
1. Every `nod` inside k8s cluster has unique **ip address** which is called nod ip address.  
2. Every `pod` inside k8s cluster nod has unique **port number**       
3. The ip address of nod and port number of pod is use for communication and sharing resources.     
### Inter-pod communication   
1. All the pod have unique ip address.    
2. The port ip address are fully routable on the **pod network** inside k8s cluster.  
3. Their is no need for mapping the port.
4. The communicate the container inside the specific pod then **port ip.port numner**  

####   


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
