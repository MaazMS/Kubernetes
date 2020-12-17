### why we need volume  
1. How can data persist through-out lifecycle of pod?.  
2. How can data persist beyond lifecycle of pod?.   
3. How can container share files between container pod?.    

### volume  
1. pods are stateless or stateful.  
`stateless`   
If create the pod and pod is die for some reason, then pod is re-create and schedule any other node inside the cluster,   
for that reason we should create pod is stateless. It provide flexibility to run pods any node inside cluster.   
`stateful`   
The app inside the pod is deal with data then those app called as stateful app. eg. web app.   
2. k8s provide volume for stateful apps.      
3. At its core, a volume is just a directory, possibly with some data in it, which is accessible to the containers in a pod.  
3. volume bring persistence to pods.  
4. create pod with single container or Multiple container attach volume, then all container access volume.      
5. volume are associated with lifecycle of pod.    
6. k8s support many types of volume.  

### volume types   
1. Ephemeral (same lifetime as pod)  
2. Durable (Beyonds pods lifetime)  

**Ephemeral**  
Ephemeral volume create when pod is created, when pod die Ephemeral volume is destroy.  
**Durable** 
1. Durable volume create when pod is created, but data persist inside the volume even after pod die.   
2.We can refer this volume another new pod with to make use of data exit already and create new data on top of that volume.  