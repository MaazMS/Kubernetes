# ReplicaSet 
* It ensure that a specific numbers of pods are running at any point of time.   
* In case that their are too many pods are running what was define in mainfest file, then relicaset will terminate extra  pods.  
* In case that their are less pod are running what was define in mainfest file, then replicaset will create pod.   
* Some times pod is fail, deleted or some other issue and if it back by replicaset then this pod re-created automatically on same nod or helping nod.     
* In some situation one pod run all the time, then we define **replica context** one in mainfest file.  

Q1. How the replicaset is mange the pod are aware of the pod and what is technique between replicaset and pod.?   
ans : Replocaset and pod are associated with `labels` 

### Replicaset vs   Replication controller
Replicaset | Replication controller  |
---- | ----|
Replicaset is next generation of Replication controller |  generation of Replication controller previous generation 
both have same purpose | both have same purpose
new version | old version 
support set based selector | Equality based selector    

### Label and selector  
**Label**   
1. Label are key value pair generally attached to pod.  
2. It is use to give tag to pod.  
3. It is helping to manage and display pod.
**selector** 
1. Controller and services are manage pods using selector.  
2. Their are two way to define selector.  

### selector vs selector matchLabels   
```` 
selector:                                     selector: 
    app: nginx                                matchLabels: 
    tier: front-end                                app: nginx  
                                                   tier: front-end


```` 
support for older resource such as            support for new resource such as ReplicaSet, deployment, job, deamonset.   
Replication controller, services.  

### Equilty-based and Set-based Selector.  
![](https://github.com/MaazMS/Kubernetes/blob/k8s/components_doc/images/Enqulity%20set%20based.png?raw=true)   