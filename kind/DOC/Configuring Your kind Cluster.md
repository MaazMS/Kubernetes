### create yaml file   
* It is help full to create cluster with any number of worker nodes and master nodes.  
`maaz@maaz-Lenovo-G50-70:~$ vi kind-ex1-config.yaml`    
* inside of kind-ex1-config.yaml    
````
kind: Cluster    
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
- role: worker
- role: worker
- role: worker
- role: worker

````  
* it show extra node i have create 6 nodes but here is show 7 nodes.  
```
maaz@maaz-Lenovo-G50-70:~$ kind get nodes 
kind-control-plane
kind-worker4
kind-worker
kind-worker5
kind-worker3
kind-worker2
kind-worker6

```
* because all nodes is communicating, and shareing resource with helo of loadbalancer node.   

