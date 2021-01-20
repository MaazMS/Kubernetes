### elasticsearch 
1. create yaml file inside that 
````
apiVersion: elasticsearch.k8s.elastic.co/v1
kind: Elasticsearch
metadata:
  name: quickstart
spec:
  version: 7.10.2
  nodeSets:
  - name: default
    count: 1elasticsearch
    config:
      node.store.allow_mmap: false
````
2. apply elasticsearch ` kubectl apply -f fileName.yaml`   
3. `node.store.allow_mmap: false` This is use for production environment.  
### check elastic search 
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$` **kubectl get elasticsearch**

``` 
NAME         HEALTH   NODES   VERSION   PHASE   AGE
quickstart   green    1       7.10.2    Ready   43m
```
### check the pods for elasticsearch 
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$` **kubectl get pods**  
```
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   0          44m
```

### check the logs for elasticsearch
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$` **kubectl logs -f quickstart-es-default-0**
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl logs -f quickstart-es-default-0 
{"timestamp": "2021-01-20T08:51:59+00:00", "message": "readiness probe failed", "curl_rc": "7"}
{"timestamp": "2021-01-20T08:52:00+00:00", "message": "readiness probe failed", "curl_rc": "7"}
```
### change version of elasticsearch 
1. If change elasticsearch new version to old version it show error. 
* check elasticsearch pod
```  
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get po
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   0          56m
```
* check the version of elasticsearch version with name of kind in yaml file
````
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get Elasticsearch
NAME         HEALTH   NODES   VERSION   PHASE   AGE
quickstart   green    1       7.10.2    Ready   4m48s
------------------------------------------------------------------
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get elasticsearch
NAME         HEALTH   NODES   VERSION   PHASE   AGE
quickstart   green    1       7.10.2    Ready   4m48s
````
* change version 7.10.2 to 7.10.1
````   
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply -f elastic1.yaml 
Error from server (Elasticsearch.elasticsearch.k8s.elastic.co "quickstart" is invalid: spec.version: Invalid value: "7.10.1": Downgrades are not supported): error when applying patch:
{"metadata":{"annotations":{"kubectl.kubernetes.io/last-applied-configuration":"{\"apiVersion\":\"elasticsearch.k8s.elastic.co/v1\",\"kind\":\"Elasticsearch\",\"metadata\":{\"annotations\":{},\"name\":\"quickstart\",\"namespace\":\"default\"},\"spec\":{\"nodeSets\":[{\"config\":{\"node.store.allow_mmap\":false},\"count\":1,\"name\":\"default\"}],\"version\":\"7.10.1\"}}\n"}},"spec":{"nodeSets":[{"config":{"node.store.allow_mmap":false},"count":1,"name":"default"}],"version":"7.10.1"}}
to:


Resource: "elasticsearch.k8s.elastic.co/v1, Resource=elasticsearches", GroupVersionKind: "elasticsearch.k8s.elastic.co/v1, Kind=Elasticsearch"
Name: "quickstart", Namespace: "default"
for: "elastic1.yaml": admission webhook "elastic-es-validation-v1.k8s.elastic.co" denied the request: Elasticsearch.elasticsearch.k8s.elastic.co "quickstart" is invalid: spec.version: Invalid value: "7.10.1": Downgrades are not supported
````

* It mean you can upgrade the version of elasticsearch using ECK.  
* i am try by change version 7.10.1 to 7.10.2 
* create yaml file of elasticsearch with version 7.10.1 
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply  -f elastic1.yaml 
elasticsearch.elasticsearch.k8s.elastic.co/quickstart created
```
* Check the version of elasticsearch
```` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get elasticsearch
NAME         HEALTH    NODES   VERSION   PHASE   AGE
quickstart   unknown           7.10.1            16s
````
* upgrade the version of elasticsearch
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply  -f elastic1.yaml 
elasticsearch.elasticsearch.k8s.elastic.co/quickstart configured
```
* check upgrade of elasticsearch pods
```` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          39m
quickstart-es-default-1   1/1     Running   1          26m
````
* decrease the pod of elasticsearch 
```` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get elasticsearch
NAME         HEALTH    NODES   VERSION   PHASE   AGE
quickstart   unknown           7.10.2    Ready   39m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl pod
Error: unknown command "pod" for "kubectl"

Did you mean this?
        top

Run 'kubectl --help' for usage.
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          39m
quickstart-es-default-1   1/1     Running   1          26m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get Elasticsearch
NAME         HEALTH    NODES   VERSION   PHASE   AGE
quickstart   unknown           7.10.2    Ready   40m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply -f elastic1.yaml 
elasticsearch.elasticsearch.k8s.elastic.co/quickstart configured
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          42m
quickstart-es-default-1   1/1     Running   1          29m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          42m
quickstart-es-default-1   1/1     Running   1          29m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          42m
quickstart-es-default-1   1/1     Running   1          29m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          42m
quickstart-es-default-1   1/1     Running   1          29m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          43m
quickstart-es-default-1   1/1     Running   1          29m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get Elasticsearch
NAME         HEALTH    NODES   VERSION   PHASE   AGE
quickstart   unknown           7.10.2    Ready   44m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          43m
quickstart-es-default-1   1/1     Running   1          29m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply -f elastic1.yaml 
elasticsearch.elasticsearch.k8s.elastic.co/quickstart unchanged
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          43m
quickstart-es-default-1   1/1     Running   1          30m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl get  pod
NAME                      READY   STATUS    RESTARTS   AGE
quickstart-es-default-0   1/1     Running   1          44m
quickstart-es-default-1   1/1     Running   1          30m
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply -f elastic1.yaml 
The Elasticsearch "quickstart" is invalid: spec.nodeSets.count: Invalid value: 1: spec.nodeSets.count in body should be greater than or equal to 1
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ kubectl apply -f elastic1.yaml 
````
#### Elasticsearch services 
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ ` **kubectl get svc**   
```  
NAME                      TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
kubernetes                ClusterIP   10.96.0.1      <none>        443/TCP    3h11m
quickstart-es-default     ClusterIP   None           <none>        9200/TCP   52m
quickstart-es-http        ClusterIP   10.96.245.55   <none>        9200/TCP   52m
quickstart-es-transport   ClusterIP   None           <none>        9300/TCP   52m
```
**Note** `quickstart-es-http` This service is used for http service.   

### elasticsearch secret 
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK/Elasticsearch$ ` **kubectl get secret**  
```` 
NAME                                   TYPE                                  DATA   AGE
default-token-jwvc2                    kubernetes.io/service-account-token   3      3h46m
quickstart-es-default-es-config        Opaque                                1      87m
quickstart-es-elastic-user             Opaque                                1      10m
quickstart-es-http-ca-internal         Opaque                                2      87m
quickstart-es-http-certs-internal      Opaque                                3      87m
quickstart-es-http-certs-public        Opaque                                2      10m
quickstart-es-internal-users           Opaque                                2      87m
quickstart-es-remote-ca                Opaque                                1      87m
quickstart-es-transport-ca-internal    Opaque                                2      87m
quickstart-es-transport-certificates   Opaque                                5      87m
quickstart-es-transport-certs-public   Opaque                                1      10m
quickstart-es-xpack-file-realm         Opaque                                3      87m

````
### username and password are store 
1. This secret have username and password
`quickstart-es-elastic-user             Opaque                                1      10m`
### Getting the credentials(username and password). 
1. name is elastic
2. password is encrypted that way it decode usnig base64
````
maaz@maaz-Lenovo-G50-70:~$  PASSWORD=$(kubectl get secret quickstart-es-elastic-user -o go-template='{{.data.elastic | base64decode}}')
maaz@maaz-Lenovo-G50-70:~$ echo $PASSWORD
50xpvg9nf07eAAr0U55W5FB8
````
### Access elasticsearch using browser 
1. name is elastic
2. password 50xpvg9nf07eAAr0U55W5FB8
``` 
{
  "name" : "quickstart-es-default-0",
  "cluster_name" : "quickstart",
  "cluster_uuid" : "8SFx9jAuQ4yRExpNCrSlwA",
  "version" : {
    "number" : "7.10.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "747e1cc71def077253878a59143c1f785afa92b9",
    "build_date" : "2021-01-13T00:42:12.435326Z",
    "build_snapshot" : false,
    "lucene_version" : "8.7.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```
### Request the Elasticsearch endpoint 
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kubectl port-forward service/quickstart-es-http  9200


`
