### why we need Persistent Volumes  
1. company's infrastructure  team provide different storage solution such as Block, NAS, Object storage, Google Cloud disk,  
AWS Disk etc.  
2. There we need to be a consistency way to deal with all these storage types?.    
3. Different type of storage have different architecture and different API, problem is here is that if you attach and manage   
these storage types manually we have to develop custom plugins to interact with external derives apis.   
4. There for we need one storage interface for all durable storage option k8s solution is Persistent Volumes.  
### Persistent Volumes    
1. Storage management system.  
2. pv subsystem provide a standard API for developer and administrator that abstract details from how it consumed.  
3. Then developer focus on storage capacity and storage type their application is running rather then each and every of   
storage provide by APIs k8s provide two API object Persistent Volumes(pv) and Persistent Volumes claim(pvc).  

`Persistent Volumes`   
1. Persistent Volumes is a piece of pre provision storage inside the cluster.    
2. Typically previsioned by administrator.  
3. Tha data inside these volume can exist beyond the lifecycle of individual port that gives us this pv.  
     
 `Persistent Volumes claim`   
 1. Persistent Volumes claim is a storage request by developer with some mode such as read and write .    
 
 ###  Lifecyle of Persistent volume.    
step 1: provision  
Administrator create storage volume and these volume can any storage type. This volume called Persistent volume.  
step 2: binding  
We bind the storage request to Persistent volume, this storage request is celled Persistent volume claim.  
Q1. How pvc is binding the pv?.  
case 1: Developer request 100GB but pv size is 50GB then pvc is wait until pv is create 100GB.  
case 2: Developer request 10GB but pv size is 12GB then pvc is binding to pv.   
step 3: Using  
pvc is bonded to pv then k8s create port and application team start using volume inside pod.  
step 4: Reclaiming   
Developer delete pvc k8s  

### prevision storage volume inside k8s two types   
1. static   
2. dynamic   
  
**static**  
1. Administrator need to create the Persistent volume before developer Persistent volume claim by developer.  
2. When user is request the storage which is not available then dynamic storage come.      
**dynamic**  
1. Storage infrastructure with different types of storage such as fast ssd ,slow speed HDD, distributed  cluster storage  
so we do not create pv manually instead we create storage class these storage class are generally created depending upon   
the type of medium in the backend.    
2. These storage class created and configured by admin and this is one time setup not create pv manually all the time.  
3. Admin will have to configure the default storage class before we do any things.  
4. This is useful when developer does not mention storage class inside pvc configure. It automatically provisioned storage    
from default storage class.  
      