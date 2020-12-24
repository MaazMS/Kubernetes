### 
maaz@maaz-Lenovo-G50-70:~$ kind help   
kind creates and manages local Kubernetes clusters using Docker container 'nodes    

``` 
Available Commands:
  build       Build one of [node-image]
  completion  Output shell completion code for the specified shell (bash, zsh or fish)
  create      Creates one of [cluster]
  delete      Deletes one of [cluster]
  export      Exports one of [kubeconfig, logs]
  get         Gets one of [clusters, nodes, kubeconfig]
  help        Help about any command
  load        Loads images into nodes
  version     Prints the kind CLI version
```   

`maaz@maaz-Lenovo-G50-70:~$ kind create --help`  
### How to create cluster     
maaz@maaz-Lenovo-G50-70:~$ kind create cluster      
``` 

 ✓ Ensuring node image (kindest/node:v1.19.1)    🖼 
 ✓ Preparing  📦            
 ✓ Writing configuration 📜         
 ✓ Starting control-plane 🕹️            
 ✓ Installing CNI 🔌               
 ✓ Installing StorageClass 💾             
Set kubectl context to "kind-kind"            
You can now use your cluster with:          

kubectl cluster-info --context kind-kind          

Thanks for using kind! 😊              

```
1. Download The image (k8s cluster)     
2. Preparing nodes (worker node)
3. configuration setup (kube-configuration)
4. Starting control-plane (master node)  
5. Installing CNI (Container Network Interface) 
6. Installing StorageClass   

* creating cluster by user define name   

**maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kind create cluster --name test1**  
``` 
Creating cluster "test1" ...
 ✓ Ensuring node image (kindest/node:v1.19.1) 🖼 
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-test1"
You can now use your cluster with:

kubectl cluster-info --context kind-test1

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂
```
**maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/ECK$ kind get clusters**    
test1


### configuration of cluster   
1. To see kube-configuration file`kind get kubeconfig`

### Details of inside cluster nodes  
* small details of nodes  
```
maaz@maaz-Lenovo-G50-70:~$ kubectl get nodes
NAME                 STATUS   ROLES    AGE     VERSION
kind-control-plane   Ready    master   2m34s   v1.19.1

```
*  full details of nodes  
```` 
maaz@maaz-Lenovo-G50-70:~$ kubectl  get nodes -o wide
NAME                 STATUS   ROLES    AGE    VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE                                     KERNEL-VERSION     CONTAINER-RUNTIME
kind-control-plane   Ready    master   129m   v1.19.1   172.18.0.2    <none>        Ubuntu Groovy Gorilla (development branch)   5.4.0-58-generic   containerd://1.4.0
````   
* client and server details are showing k8s cluster version   
```
maaz@maaz-Lenovo-G50-70:~$ kubectl version --short
Client Version: v1.20.0
Server Version: v1.19.1
```   
* kubernetes system details  
````
maaz@maaz-Lenovo-G50-70:~$ kubectl -n kube-system get all 
NAME                                             READY   STATUS    RESTARTS   AGE
pod/coredns-f9fd979d6-tmxkg                      1/1     Running   0          132m
pod/coredns-f9fd979d6-zcdc6                      1/1     Running   0          132m
pod/etcd-kind-control-plane                      1/1     Running   0          132m
pod/kindnet-wrcwl                                1/1     Running   0          132m
pod/kube-apiserver-kind-control-plane            1/1     Running   0          132m
pod/kube-controller-manager-kind-control-plane   1/1     Running   0          132m
pod/kube-proxy-vvcnv                             1/1     Running   0          132m
pod/kube-scheduler-kind-control-plane            1/1     Running   0          132m

NAME               TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns   ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP,9153/TCP   132m

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/kindnet      1         1         1       1            1           <none>                   132m
daemonset.apps/kube-proxy   1         1         1       1            1           kubernetes.io/os=linux   132m

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/coredns   2/2     2            2           132m

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/coredns-f9fd979d6   2         2         2       132m

````


### how to delete cluster   
1. kind delete cluster.  
kind will use the default cluster context name kind and delete that cluster.    
``` 
maaz@maaz-Lenovo-G50-70:~$ kind get clusters 
kind  
maaz@maaz-Lenovo-G50-70:~$ kind delete clusters test1
Deleted clusters: ["kind"]
``` 
2. Delete the name of specific cluster  
```   
maaz@maaz-Lenovo-G50-70:~$ kind get clusters
test1
maaz@maaz-Lenovo-G50-70:~$ kind delete clusters test1
Deleted clusters: ["test1"]
maaz@maaz-Lenovo-G50-70:~$ kind get clusters
No kind clusters found.

```

Q. creating images   