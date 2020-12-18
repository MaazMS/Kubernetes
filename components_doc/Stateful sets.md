### Stateful sets  
1. It is use for Stateful application.  
2. Stateful application : Are those application that store data in database for track the state of the application.    
3. There are two way to deploy the application   1. `deployment` 2.`Stateful`    
4. Stateless application is deploy using deployment.     
5. StatefulSet is the workload API object used to manage stateful applications.  
6. StatefulSet manages Pods that are based on an identical container spec.  
7. When using Kubernetes, most of the time you don’t care how your pods are scheduled, but sometimes you care that pods   
are deployed in order, that they have a persistent storage volume, or that they have a unique, stable network identifier   
across restarts and reschedules. In those cases, StatefulSets can help you accomplish your objective.     

### Using StatefulSets   
1. Stable, unique network identifiers.  
2. Stable, persistent storage.
3. Ordered, graceful deployment and scaling.
4. Ordered, automated rolling updates.   



    
  