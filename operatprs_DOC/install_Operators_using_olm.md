
* The first step is to define an OperatorGroup to dictate which namespaces the Operator will manage.  
* Create the group using the kubectl.    

Check information of operators **kubectl describe packagemanifest/etcd -n olm**   
**Alm - Examples:**  
* series of manifests that you can use to deploy custom resources defined by this Operator.  
**Install Modes**  
* install modes section describes the circumstances in which an end user may deploy this Operator.    
**which Namespace is Supported**   
``` 
 Type:       OwnNamespace
 Supported:  false
 Type:       SingleNamespace
 Supported:  false

``` 
**The Name field in this section indicates the name of the channel which is referenced by a subscription.** 
``` 
 Name:           singlenamespace-alpha
  Default Channel:  singlenamespace-alpha
  Package Name:     etcd
  Provider:
    Name:  CNCF
```  
**Once you have decided on a channel, the last step is to create the subscription resource itself.**     
    
            
* create elastic-cloud-eck.yaml  
````
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ wget https://operatorhub.io/install/elastic-cloud-eck.yaml
--2020-12-22 14:08:12--  https://operatorhub.io/install/elastic-cloud-eck.yaml
Resolving operatorhub.io (operatorhub.io)... 23.212.253.51, 23.212.253.49
Connecting to operatorhub.io (operatorhub.io)|23.212.253.51|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 227 [text/html]
Saving to: ‘elastic-cloud-eck.yaml’

elastic-cloud-eck.yaml              100%[=================================================================>]     227  --.-KB/s    in 0s      

2020-12-22 14:08:14 (4.50 MB/s) - ‘elastic-cloud-eck.yaml’ saved [227/227]


````  
* How to read csv   
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ cat elastic-cloud-eck.yaml 
apiVersion: operators.coreos.com/v1alpha1
kind: Subscription
metadata:
  name: my-elastic-cloud-eck
  namespace: operators
spec:
  channel: stable
  name: elastic-cloud-eck
  source: operatorhubio-catalog
  sourceNamespace: olm
``` 
* operators status     
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl get pod -n operators
NAME                                READY   STATUS    RESTARTS   AGE
elastic-operator-776fc7b64c-9xp2w   1/1     Running   0          32m
``` 
* csv in my etcd   
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl get csv -n my-etcd -w
NAME                       DISPLAY                        VERSION   REPLACES                   PHASE
elastic-cloud-eck.v1.3.1   Elasticsearch (ECK) Operator   1.3.1     elastic-cloud-eck.v1.3.0   Succeeded
etcdoperator.v0.9.4        etcd                           0.9.4     etcdoperator.v0.9.2        Succeeded
```
* 
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl apply -f elastic-cloud-eck.yaml
subscription.operators.coreos.com/my-elastic-cloud-eck unchanged
```  

* 
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl apply -f elastic-cloud-eck.yaml 
Warning: resource subscriptions/my-elastic-cloud-eck is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
subscription.operators.coreos.com/my-elastic-cloud-eck configured
```  
*  
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl create -f https://operatorhub.io/install/elastic-cloud-eck.yaml
subscription.operators.coreos.com/my-elastic-cloud-eck created
```