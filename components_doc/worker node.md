* worker node is nothing but virtual machine or physical machine.    
* They expose the underlying compute, networking, and storage etc to the application.  
* All Those node join together to form the cluster.     

**1.Kubelet**   
* Responsible for maintaining a set of pods, which are composed of one or more containers, on a local system.           
* kubelet functions as a local agent that watches for pod specs via the Kubernetes API server.   
* In case If kubelet noticed any issue with pods running on the worker node, then it tries to restart port on same node.    
* In case of an issue with a worker node itself then in this case k8s and its master detects an failure then it decides   
to recreate the pods and other healthy nodes.     

**2.Kube-proxy**   
* It is critical element inside for responsible the entire network configuration.   
* It essentially maintains the distributed network across all the nodes across all the pods and across all the containers.   
* It also exposes services to outside the world.  

**3. pod**  
1. It is scheduling unit.  
2. Each pod consist of one and more container.  

**4. Container**  
1. Runtime environment for containerized applications.   
2. These container is inside the pod.  
3. It design to run micro services.    
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/worker.png?raw=true)     


