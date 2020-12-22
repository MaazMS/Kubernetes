### installing olm  
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ curl -L https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.17.0/install.sh -o install.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   636  100   636    0     0   1156      0 --:--:-- --:--:-- --:--:--  1156
100  1286  100  1286    0     0    649      0  0:00:01  0:00:01 --:--:--  1065
```
* create executable file
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ chmod +x install.sh`  
* install the executable file   
`maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ ./install.sh v0.17.0 `  
* check olm  
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl get ns olm
NAME   STATUS   AGE
olm    Active   7m53s

``` 
* number of pod in olm   
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl get pods -n olm
NAME                                READY   STATUS    RESTARTS   AGE
catalog-operator-598b54c95d-j7wfn   1/1     Running   0          8m10s
olm-operator-fb46b989d-8fhgx        1/1     Running   0          8m10s
operatorhubio-catalog-zm7mg         1/1     Running   0          7m1s
packageserver-65c66b64c-g7nf6       1/1     Running   1          6m57s
packageserver-65c66b64c-xkw98       1/1     Running   1          6m57s
```  
* crd in olm   
```
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes$ kubectl get crd
NAME                                          CREATED AT
catalogsources.operators.coreos.com           2020-12-22T07:06:37Z
clusterserviceversions.operators.coreos.com   2020-12-22T07:06:38Z
installplans.operators.coreos.com             2020-12-22T07:06:39Z
operatorgroups.operators.coreos.com           2020-12-22T07:06:39Z
operators.operators.coreos.com                2020-12-22T07:06:39Z
subscriptions.operators.coreos.com            2020-12-22T07:06:40Z

```