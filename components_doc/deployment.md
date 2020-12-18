### why need deployment
Q1. Imagine your are upgrading application from v1 to v2.   
a. upgrading with zero downtime?.    
b. upgrading sequentially, one after another?.      
c. paused and resume upgrad process?.  
d. Rollback upgrade to previous stable release?.  

### Deployment 
1. Deployment is the controller.  
2. Deployment is all about **Update** and **Rollbacks**  
3. It provide declarative updates for pods and replicaset.  
4. It upgrade the version of app and also increase and decrease number of pod replica.  
5. we define pod, replicaset, deployment in one mainfest file.  
6. inside deployment mainfest file contain pod definition , number of pod relicaset, upgrade strategy.  

### Feature  
1. Multiple Replicas    
2. Upgrade  
3. Rollback  
4. Scale up or down 
5. Pause and Resume  

**Multiple Replicas**     
With the help of deployment we can create multiple replicas of pods for high availability and load balancing.  
when we create deployment by default k8s automatically create replicaset in the background for you.  
In case we not mention replicaset in deployment mainfest file, deployment will create replicaset with count 1.Because   
it safe that one pod is running always.     
**Upgrade** 
**Rollback**  
if some things wrong with current upgrade then deployment controller will allow to rollback to you previous stable version.  
**Scale up or down**    
Once we deploy the application  we can scale up or down application instances based on load. For this just you do it upgrade   
replica field in deployment mainfest file.  
**Pause and Resume** 
we can pause deployment processing progress as we needed you can use this feature test and validate new version of thre app.  

### Deployment Types 
1. Recreate   
2. RollingUpdate  
3. canary  
4. Blue / Green  

**Recreate**   
Assume that we update version A to version B. Recreate is the demy  deployment which consist of shadding down version A   
and after making sure version A is turn off, then you start deployment version B.(down time of services)    

**RollingUpdate**  
slowly upgrade the app by replacing instances one after another until all the instances are successfully role out.  
It is default strategy for k8s.  
**canary**  
It is use when you want to not upgrade the full app at one.  
first update the 2 or 3 instances of app it work successful then upgrade remmaning instances of app.  
After that terminate the old version.  
**Blue / Green** 
Using this deployment method version B which is green is deploy along side the version A which is Blue.  
With exactly same amount of instances so after testing new version meet all the requirement the traffic is switch from  
version A to version B at load balance level. 
Benefit is instance rollout and rollback.  
  