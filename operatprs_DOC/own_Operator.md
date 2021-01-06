### overview 
1. Operator SDK released by CoreOS is a brilliant tool for writing your own operator from scratch.  
2. It provides the necessary boilerplate code and a high level abstract to communicate with the Kubernetes API.  
* Writing a custom operator using this SDK has the following steps:   
1. Design your own Custom Resource YAML file that will be read by the operator.  
2. Write code to consume this new Resource kind.  
3. Add logic on what to deploy/update native K8s resources and when to do that.   

### installing of operator SDK  
1. goto github.com search operator sdk and open official page.   
2. `wget https://github.com/operator-framework/operator-sdk/releases/download/v1.3.0/operator-sdk_linux_amd64`    
3. sudo mv operator-sdk_linux_amd64 /usr/local/bin/operator-sdk
3. create executable file. `sudo chmod +x /usr/local/bin/operator-sdk`  
4. check patch 
``` 
echo $PATH
cd /usr/local/bin/operator-sdk
```  
5. full details about operator sdk 
``` 
maaz@maaz-Lenovo-G50-70:~/github/operator$ which operator-sdk
/usr/local/bin/operator-sdk 
maaz@maaz-Lenovo-G50-70:~/github/operator$ operator-sdk version
operator-sdk version: "v1.3.0", commit: "1abf57985b43bf6a59dcd18147b3c574fa57d3f6", kubernetes version: "1.19.4", go version: "go1.15.5", GOOS: "linux", GOARCH: "amd64" 
```

#### Operator SDK with Go   
1. create directory `mkdir operator`   
1. To initialize the project using command.  
`maaz@maaz-Lenovo-G50-70:~/github/operator$ operator-sdk init --domain=example.com --repo=github.com/MaazMS/operator-SDK-go`     
        
output 
````
Writing scaffold for you to edit...
Get controller runtime:
$ go get sigs.k8s.io/controller-runtime@v0.7.0
Update go.mod:
$ go mod tidy
Running make:
$ make
go: creating new go.mod: module tmp
Downloading sigs.k8s.io/controller-tools/cmd/controller-gen@v0.4.1
go: finding sigs.k8s.io v0.4.1
go: finding sigs.k8s.io/controller-tools/cmd/controller-gen v0.4.1
go: finding sigs.k8s.io/controller-tools/cmd v0.4.1
/home/maaz/github/operator/bin/controller-gen object:headerFile="hack/boilerplate.go.txt" paths="./..."
go fmt ./...
go vet ./...
go build -o bin/manager main.go
Next: define a resource with:
$ operator-sdk create api 

````    
* Error    
`Error: failed to initialize project with "go.kubebuilder.io/v3": only the go.mod and files with the prefix "(.)" are allowed before the init`
* solution `https://github.com/operator-framework/operator-sdk/issues/4355`       
`operator-sdk init --domain=test.com --repo=github.com/MaazMS/operator-SDK-go --plugins go.kubebuilder.io/v2 `  

1. These files are created when initialize operator sdk project.  
```  
.
├── bin
│   └── manager
├── config
│   ├── certmanager
│   │   ├── certificate.yaml
│   │   ├── kustomization.yaml
│   │   └── kustomizeconfig.yaml
│   ├── default
│   │   ├── kustomization.yaml
│   │   ├── manager_auth_proxy_patch.yaml
│   │   ├── manager_webhook_patch.yaml
│   │   └── webhookcainjection_patch.yaml
│   ├── manager
│   │   ├── kustomization.yaml
│   │   └── manager.yaml
│   ├── prometheus
│   │   ├── kustomization.yaml
│   │   └── monitor.yaml
│   ├── rbac
│   │   ├── auth_proxy_client_clusterrole.yaml
│   │   ├── auth_proxy_role_binding.yaml
│   │   ├── auth_proxy_role.yaml
│   │   ├── auth_proxy_service.yaml
│   │   ├── kustomization.yaml
│   │   ├── leader_election_role_binding.yaml
│   │   ├── leader_election_role.yaml
│   │   └── role_binding.yaml
│   ├── scorecard
│   │   ├── bases
│   │   │   └── config.yaml
│   │   ├── kustomization.yaml
│   │   └── patches
│   │       ├── basic.config.yaml
│   │       └── olm.config.yaml
│   └── webhook
│       ├── kustomization.yaml
│       ├── kustomizeconfig.yaml
│       └── service.yaml
├── Dockerfile
├── go.mod
├── go.sum
├── hack
│   └── boilerplate.go.txt
├── main.go
├── Makefile
└── PROJECT

12 directories, 34 files

```
1.Creating the API and Controller , resources 
`maaz@maaz-Lenovo-G50-70:~/github/operator$ operator-sdk create api --group=app --version=v1alpha1 --kind=PodSet --resource --controller`  
  
output  
``` 
Writing scaffold for you to edit...
api/v1alpha1/podset_types.go
controllers/podset_controller.go
Running make:
$ make
/home/maaz/github/operator/bin/controller-gen object:headerFile="hack/boilerplate.go.txt" paths="./..."
go fmt ./...
go vet ./...
go build -o bin/manager main.go
```   
1. These files are created when create api.     
```  
.
├── api
│   └── v1alpha1
│       ├── groupversion_info.go
│       ├── podset_types.go
│       └── zz_generated.deepcopy.go
├── bin
│   ├── controller-gen
│   └── manager
├── config
│   ├── certmanager
│   │   ├── certificate.yaml
│   │   ├── kustomization.yaml
│   │   └── kustomizeconfig.yaml
│   ├── crd
│   │   ├── kustomization.yaml
│   │   ├── kustomizeconfig.yaml
│   │   └── patches
│   │       ├── cainjection_in_podsets.yaml
│   │       └── webhook_in_podsets.yaml
│   ├── default
│   │   ├── kustomization.yaml
│   │   ├── manager_auth_proxy_patch.yaml
│   │   └── manager_config_patch.yaml
│   ├── manager
│   │   ├── controller_manager_config.yaml
│   │   ├── kustomization.yaml
│   │   └── manager.yaml
│   ├── prometheus
│   │   ├── kustomization.yaml
│   │   └── monitor.yaml
│   ├── rbac
│   │   ├── auth_proxy_client_clusterrole.yaml
│   │   ├── auth_proxy_role_binding.yaml
│   │   ├── auth_proxy_role.yaml
│   │   ├── auth_proxy_service.yaml
│   │   ├── kustomization.yaml
│   │   ├── leader_election_role_binding.yaml
│   │   ├── leader_election_role.yaml
│   │   ├── podset_editor_role.yaml
│   │   ├── podset_viewer_role.yaml
│   │   └── role_binding.yaml
│   ├── samples
│   │   ├── app_v1alpha1_podset.yaml
│   │   └── kustomization.yaml
│   └── scorecard
│       ├── bases
│       │   └── config.yaml
│       ├── kustomization.yaml
│       └── patches
│           ├── basic.config.yaml
│           └── olm.config.yaml
├── controllers
│   ├── podset_controller.go
│   └── suite_test.go
├── Dockerfile
├── go.mod
├── go.sum
├── hack
│   └── boilerplate.go.txt
├── main.go
├── Makefile
└── PROJECT

17 directories, 45 files
``` 
1. [got to this topic important before going to next step](let's-discuss-about-spec-and-status.)     
1. after that update `zz_generated.deepcopy.go` using `make generate`  
1. Then generate our customized CRD and additional object YAMLs. using `make manifests`   
1. [Customizing the Operator Logic](Customizing-the-Operator-Logic)
### let's discuss about spec and status.   
1. Every functional object is k8s include `spec` and `status`.  
1. operator sdk is reconciling the describe state with actual cluster state.   
1. location for this code ` api/v1alpha1/podset_types.go`    
1. Deploy your PodSet Custom Resource Definition `kubectl apply -f config/crd/bases/app.example.com_podsets.yaml`  
1. Confirm the CRD was successfully created `kubectl  get crd podsets.app.example.com -o yaml`  
1. install operator `make install`    
```
maaz@maaz-Lenovo-G50-70:~/github/operator$ make install
/home/maaz/github/operator/bin/controller-gen "crd:trivialVersions=true,preserveUnknownFields=false" rbac:roleName=manager-role webhook paths="./..." output:crd:artifacts:config=config/crd/bases
/home/maaz/github/operator/bin/kustomize build config/crd | kubectl apply -f -
customresourcedefinition.apiextensions.k8s.io/podsets.app.example.com created

````  
1. run operator `make run`  
```  
maaz@maaz-Lenovo-G50-70:~/github/operator$ make run
/home/maaz/github/operator/bin/controller-gen object:headerFile="hack/boilerplate.go.txt" paths="./..."
go fmt ./...
go vet ./...
/home/maaz/github/operator/bin/controller-gen "crd:trivialVersions=true,preserveUnknownFields=false" rbac:roleName=manager-role webhook paths="./..." output:crd:artifacts:config=config/crd/bases
go run ./main.go
2021-01-04T12:53:46.627+0530	INFO	controller-runtime.metrics	metrics server is starting to listen	{"addr": ":8080"}
2021-01-04T12:53:46.628+0530	INFO	setup	starting manager
2021-01-04T12:53:46.628+0530	INFO	controller-runtime.manager	starting metrics server	{"path": "/metrics"}
2021-01-04T12:53:46.628+0530	INFO	controller-runtime.manager.controller.podset	Starting EventSource	{"reconciler group": "app.example.com", "reconciler kind": "PodSet", "source": "kind source: /, Kind="}
2021-01-04T12:53:46.829+0530	INFO	controller-runtime.manager.controller.podset	Starting EventSource	{"reconciler group": "app.example.com", "reconciler kind": "PodSet", "source": "kind source: /, Kind="}
2021-01-04T12:53:46.930+0530	INFO	controller-runtime.manager.controller.podset	Starting Controller	{"reconciler group": "app.example.com", "reconciler kind": "PodSet"}
2021-01-04T12:53:46.930+0530	INFO	controller-runtime.manager.controller.podset	Starting workers	{"reconciler group": "app.example.com", "reconciler kind": "PodSet", "worker count": 1}
2021-01-04T12:53:46.945+0530	INFO	controllers.PodSet	Scaling up pods	{"Currently available": 0, "Required replicas": 3}
2021-01-04T12:53:47.016+0530	INFO	controllers.PodSet	Scaling up pods	{"Currently available": 0, "Required replicas": 3}
2021-01-04T12:53:47.056+0530	INFO	controllers.PodSet	Scaling up pods	{"Currently available": 2, "Required replicas": 3}
^C2021-01-04T13:01:17.235+0530	INFO	controller-runtime.manager.controller.podset	Stopping workers	{"reconciler group": "app.example.com", "reconciler kind": "PodSet"}
``` 
1. 
```` 
maaz@maaz-Lenovo-G50-70:~/github/operator$ kubectl get podset
NAME            AGE
podset-sample   2m1s 

maaz@maaz-Lenovo-G50-70:~/github/operator$ kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
podset-sample-pod4k27g   1/1     Running   0          70s
podset-sample-podhpf4c   1/1     Running   0          70s
podset-sample-podpbknz   1/1     Running   0          70s 

maaz@maaz-Lenovo-G50-70:~/github/operator$ kubectl get podset podset-sample -o yaml | grep podNames -A20
        f:podNames: {}
    manager: main
    operation: Update
    time: "2021-01-04T07:23:48Z"
  name: podset-sample
  namespace: default
  resourceVersion: "1622"
  selfLink: /apis/app.example.com/v1alpha1/namespaces/default/podsets/podset-sample
  uid: a93be09a-a50f-42fc-8739-bf892a53bb9e
spec:
  replicas: 3
status:
  podNames:
  - podset-sample-podpbknz
  - podset-sample-pod4k27g
  - podset-sample-podhpf4c
maaz@maaz-Lenovo-G50-70:~/github/operator$ kubectl get deployment
No resources found in default namespace. 


````
// PodSetSpec defines the desired state of PodSet
type PodSetSpec struct {
	// INSERT ADDITIONAL SPEC FIELDS - desired state of cluster
	// Important: Run "make" to regenerate code after modifying this file

	// Foo is an example field of PodSet. Edit PodSet_types.go to remove/update
	Replicas int32 `json:"replicas,omitempty"` 
}

// PodSetStatus defines the observed state of PodSet
type PodSetStatus struct {
	// INSERT ADDITIONAL STATUS FIELD - define observed state of cluster
	// Important: Run "make" to regenerate code after modifying this file
	PodNames        []string        `json:"podNames"`
    AvailableReplicas    int32    `json:"availableReplicas"`
}
````    
### Customizing the Operator Logic(Customizing-the-Operator-Logic) 

### Operator sdk Scope  

Namespaced      
Limits the Operator to managing resources in a single namespace   
Cluster   
Allows the Operator to manage resources across the entire cluster   

**Note**By default, Operators that the SDK generates are namespace-scoped.   
  
// +k8s:deepcopy-gen:interfaces=k8s.io/apimachinery/pkg/runtime.Object  
// VisitorsApp is the Schema for the visitorsapps API  
// +k8s:openapi-gen=true  
// +kubebuilder:subresource:status  
// +genclient:nonNamespaced  
type VisitorsApp struct {  
note for second last line : The tag must be before the resource type struct.    
* when creating an Operator. You can add new CRDs to an Operator using the SDK’s add api command.  
`operator-sdk add api --api-version=example.com/v1 --kind=VisitorsApp`  

crds/example_v1_visitorsapp-cr.yaml  
This is an example CR of the generated type. You’ll need to fill out the spec section with values relevant to the CRD you created.  

### 1
*_types.go file The spec object must include all possible configuration values that may be specified for resources of this type.    
Each configuration value is made up of the following:  
1. The name of the variable as it will be referenced from within the Operator code.  
1. The Go type for the variable  
1. name of the field JSON or YAML manifest users will write to create the resource.  

* types.go file Thestatus object must include all possible values that the Operator may set to convey the state of the CR.  
1. The name of the variable as it will be referenced from within the Operator code.  
1. The Go type for the variable  
1. name of the field as it will appear in the description of the CR  

### Example VisitorsApp CR:  
Size  
The number of backend replicas to create  
Title  
The text to display on the frontend web page  
### VisitorsApp CR 
BackendImage  
Indicates the image and version used to deploy the backend pods  
FrontendImage  
Indicates the image and version used to deploy the frontend pod  
``` 
The following snippet from the visitorsapp_types.go file demonstrates these additions:
type VisitorsAppSpec struct {
Size
int32 `json:"size"`
Title
string `json:"title"`
}
type VisitorsAppStatus struct {
BackendImage string `json:"backendImage"`
FrontendImage string `json:"frontendImage"`
}
The remainder of the visitorsapp_types.go file does not require any further changes.
```
you need to update any generated code using the SDK’s generate command.  

### The CRD Manifest  
The types file are useful within the Operator are made to the CRD itself.  

### Operator Permissions  
RBAC-related files and talks about how to scope the permissions to what is applicable to the Operator.  

#### Controller  
CRD and its associated types file in Go define the inbound API.  
you need a controller to watch for changes to CRs.  
The controller is responsible for “reconciling” a specific resource.  
Instead of having explicit handling for events such as add, delete, or update, the controller is passed the current      
state of the resource.  

### 
return reconcile.Result{}, nil  
The reconcile process finished with no errors and does not require another pass through the reconcile loop.  
return reconcile.Result{}, err  
The reconcile failed due to an error and Kubernetes should requeue it to try again.   
return reconcile.Result{Requeue: true}, nil  
The reconcile did not encounter an error, but Kubernetes should requeue it to run for another iteration.   
return reconcile.Result{RequeueAfter: time.Second*5}, nil
wait for the specified amount of time before requeuing the request.  

operator-sdk create api --group=app --version=v1alpha1 --kind=VisitorsApp --resource --controller
for controller kind=VisitorsApp 

type VisitorsAppSpec struct {
Size
int32 `json:"size"`
Title
string `json:"title"`
}
type VisitorsAppStatus struct {
BackendImage string `json:"backendImage"`
FrontendImage string `json:"frontendImage"`
} 

iteract with yaml , json 
by api 
sample / 
folder 
spec ;

size 
title 

mapping 
run mainfest by terminal  
changes deepcopy object.  

status check by controller not by user.  
 
go to properties crd/bases folder 
