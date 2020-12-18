### pod 
1. A pod is the smallest execution unit in Kubernetes.  
`Example `   
In the virtualization world, a virtual machine is an atomic unit and in docker world “container” is an atomic unit and In the Kubernetes world, Pods are the atomic units.     
2. It contain one or more containers and volume.   
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/small_unit_pod.png?raw=true)    
   
### pod deployment  
step 1 : write manifest file inside the mainfest file container images.  
step 2 : mainfest file submit to API-SERVER on master node.   
step 3 : master node decide deploy pod on appropriate worker nodes in k8s.   

 
* Generally our aim is deploy application in the form of container but k8s not deploy container directly on workers nods.    
* k8s is encapsulate container inside the `pod`  

Q1. What is mainfest file?.   
Kubernetes manifests are used to create, modify and delete Kubernetes resources such as pods, deployments, services or   
ingresses. It is very common to define manifests in form of . yaml files and send them to the Kubernetes API Server via   
commands such as kubectl apply -f my-file. yaml or kubectl delete -f my-file.

Q2. How scale up application?.  
a. Add new container with same pod the ans is wrong.  
b. we create new pod with same application instance in that nod.    
Q3. What happened when the nod does not have sufficient space?.  
a. create new vm and join that new nod to cluster once it ready k8s deploy pod on new nod.     
Q4. How scale down application?.  
a. delete the pod the application is scale down.           
  
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/pod%20deployment%20.png?raw=true)    

  

### Multi- container  
1. one pod for one container. which is explain above.  
2. Multi container communicate with each other directly because by referencing localhost, share same network, storage, namespace.  
 
Q1. What case we use multiple container in one single pod?.   
a. Some times we need helper container for some support task for main container that time we use multiple container.  

Q2. What type of support task we do for helper container?.   
a. processing user enter data.  
b. processing files which is uploaded by user.  

Q3. what time we create or delete helper container?.   
a. When new application create container is created also helper container.  
b. When app container die helper container is also die.  
![](https://matthewpalmer.net/kubernetes-app-developer/articles/networking-overview.png)     


### pod Networking  
1. Every `pod` inside k8s cluster has unique **ip address** which is called pod ip address.  
2. Every `container` inside pod has unique **port number**       
3. The ip address of pod and port number of container is use for communication and sharing resources.     
### Inter-pod  
1. Multiple containers from different pod communicate each other.   
2. All the pod have unique ip address.    
3. The pod ip address are fully routable on the **pod network** inside k8s cluster.  
4. Their is no need for mapping the pod.
5. The communicate the container inside the specific pod then **pod ip.port numner**  
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/Inter%20pod%20communication.png?raw=true)    
#### Intra- pod  
1. Multiple containers inside same pod communicate each other.    
2. Every `container` inside pod has unique **port number**  
3. Multiple container take share host (localhost) which is use for sharing resource.  
4. Not choose same port number in one pod.   
 ![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/Intra-%20pod%20communication.png?raw=true)    

   

# Pod lifecycle    
1. Define pod configuration inside mainfest (yml and json file)  
2. submit mainfest file to API-SERVER on k8s cluster.   
3. It get schedule on worker nodes inside the k8s cluster.  
4. once it schedule it goes to pending state.  
5. When the pod is pending state download container.    
6. pods bonds to nods and all container is created.At least one container is stilling running os is  in the process of starting or restarting.  
7. Running state the main purpose of pods is to achive task and it goe to Succeeded state.  
8. `Failed`: At least one container has failure in pod.  
9. `Unknown` : The state of the Pod cannot be determined.   
10. Pods do not "heal" or repair themselves. for example node fail and pod delete for any reason it does not replace itself.     
11. if a pod fails Kubernetes can automatically create a new replica of that pod to continue operations.  

![](https://drek4537l1klr.cloudfront.net/luksa3/v-4/Figures/6.1.png)

### pod config   
* Top 4 level required fields.  
1. API version  
2. Kind  
3. meta data   
4. spec  

`API version v1` : First stable release of API version. It contain core object which include pod, replication, controller, services.   
`API version apps/v1` : It is most common group of k8s. It include functionality tool such as deployment, replicaset, deamonset.    
`API version batch/v1 `: Object related to batch such as job.   
`Kind`: Object of k8s.                            
`meta data` : name and label.  
name : Name of object in k8s. It is not optional.   
label : It just tag give to pod. It is used to filter the pod is cluster. It is optional.  
`spec` : Define container configuration in spec.  
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/pod%20config.png?raw=true)    
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/pod_config%202.png?raw=true)   