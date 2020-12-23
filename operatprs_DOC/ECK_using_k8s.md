### Create a Kubernetes Cluster with Kind 
1. Create a cluster with a control plane and two worker nodes by running the Kind.  
````  
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kind create cluster --config kind-es-cluster.yaml
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.19.1) 🖼 
 ✓ Preparing nodes 📦 📦 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
 ✓ Joining worker nodes 🚜 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂

````
### Install the Operator Lifecycle Manager  
1. Operator Lifecycle Manager ("OLM"), a tool that helps you manage the Operators deployed to your cluster in an automated fashion.   
### Install the ECK Operator  
1. The ECK Operator provides support for managing and monitoring multiple clusters, upgrading to new stack versions,    
scaling cluster capacity, etc.  
2. Remember that the ECK Operator is a Kubernetes resource.   
   
* kubectl get CustomResourceDefinition 
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl get CustomResourceDefinition
NAME                                                 CREATED AT
apmservers.apm.k8s.elastic.co                        2020-12-23T16:12:11Z
beats.beat.k8s.elastic.co                            2020-12-23T16:12:11Z
catalogsources.operators.coreos.com                  2020-12-23T16:08:51Z
clusterserviceversions.operators.coreos.com          2020-12-23T16:08:52Z
elasticsearches.elasticsearch.k8s.elastic.co         2020-12-23T16:12:11Z
enterprisesearches.enterprisesearch.k8s.elastic.co   2020-12-23T16:12:12Z
installplans.operators.coreos.com                    2020-12-23T16:08:52Z
kibanas.kibana.k8s.elastic.co                        2020-12-23T16:12:12Z
operatorgroups.operators.coreos.com                  2020-12-23T16:08:54Z
operators.operators.coreos.com                       2020-12-23T16:08:54Z
subscriptions.operators.coreos.com                   2020-12-23T16:08:54Z
``` 
*  To see more details about a specific CRD, 
`kubectl describe CustomResourceDefinition elasticsearches.elasticsearch.k8s.elastic.co`  

* List the pods running in the elastic-system namespace with
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl get pods -n elastic-system
NAME                 READY   STATUS    RESTARTS   AGE
elastic-operator-0   1/1     Running   1          4m27s
```  
### Deploy an Elasticsearch Cluster 
Create a file called elastic-search-cluster.yaml 
``` 

``` 
* Create a two-node Elasticsearch cluster by entering the following command:   
`kubectl apply -f elastic-search-cluster.yaml  `
* see the status of the newly created Elasticsearch cluster 
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl get elasticsearch
NAME         HEALTH    NODES   VERSION   PHASE             AGE
quickstart   unknown           7.10.1    ApplyingChanges   9s
```
**NOTE**Note that the HEALTH status has not been reported yet. It takes a few minutes for the process to complete.    
Then, the HEALTH status will show as green:  
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl get elasticsearch
NAME         HEALTH   NODES   VERSION   PHASE   AGE
quickstart   green    2       7.10.1    Ready   20m
``` 
* Check the status of the pods running in your cluster with:  
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl get pods --selector='elasticsearch.k8s.elastic.co/cluster-name=quickstart'
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   0          24m
quickstart-es-default-1   1/1     Running   0          24m
```
### Verify Your Elasticsearch Installation  
* The Operator exposes the service with a static IP address   
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl get service quickstart-es-http
NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
quickstart-es-http   ClusterIP   10.96.133.101   <none>        9200/TCP   25m
```
* To forward all connections made to localhost:9200 to port 9200 of the pod running the quickstart-es-http service. 
and this command apply new terminal and not close this terminal.  
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl port-forward service/quickstart-es-http 9200
Forwarding from 127.0.0.1:9200 -> 9200
Forwarding from [::1]:9200 -> 9200
```
* Move back to the first terminal. The password for the elastic user is stored in a Kubernetes secret.
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ PASSWORD=$(kubectl get secret quickstart-es-elastic-user -o go-template='{{.data.elastic | base64decode}}')
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ echo $PASSWORD
Zv96kGG9gK8838zD05cfx5QD
``` 

**connect to Elasticsearch at https://localhost:9200** 
show window 
```
username elastic 
PASSWORD  Zv96kGG9gK8838zD05cfx5QD
``` 

### 
``` 
apiVersion: kibana.k8s.elastic.co/v1
kind: Kibana
metadata:
  name: quickstart
spec:
  version: 7.10.1
  count: 1
  elasticsearchRef:
    name: quickstart
  podTemplate:
    metadata:
      labels:
        foo: kibana
    spec:
      containers:
        - name: kibana
          resources:
            requests:
              memory: 1Gi
              cpu: 0.5
            limits:
              memory: 1Gi
              cpu: 1

```  
* create a Kibana cluster
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl apply -f kibana.yaml
kibana.kibana.k8s.elastic.co/quickstart created
```
*  you can check on the progress by running  
https://localhost:5601/