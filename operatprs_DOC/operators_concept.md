### operators concept  
1. An Operator extends Kubernetes to automate the management of the entire lifecycle
of a particular application.   
2 operators are monitor, maintain, recover, and upgrade the software they deploy.     
3. Cluster standard tools to work with Operators and the applications they manage, because Operators extend Kubernetes.   


### Operators Are Software SREs
1. Site Reliability Engineering (SRE) is a set of patterns and principles for running large systems.     
2. Teams freed from rote maintenance work have more time to create new features, fix bugs, and generally improve their products.     
3. An Operator is like an automated Site Reliability Engineer for its application.   
4. An Operator continues to monitor its application as it runs, and can back up data, recover from failures, and upgrade  
the application over time, automatically.      

### How Operators Work   
1. Operator adds an endpoint to the Kubernetes API, called a custom resource (CR), along with a control plane component   
that monitors and maintains resources of the new type.    
2. This Operator can then take action based on the resource’s state.  
3. A cluster user can interact with CRs with kubectl or another Kubernetes client, just like any other API resource.   

### Custom Resources   
1. Custom Resources as extensions of the Kubernetes API.  
2. It contain one or more fields like a native resource, but are not part of a default Kubernetes deployment.    
3. CRs hold structured data, and the API server provides a mechanism for reading and setting their fields as you would   
those in a native resource, by using kubectl or another API client.  
4. Users define a CR on a running cluster by providing a CR definition.    

### ClusterServiceVersion   
1. ClusterServiceVersion (CSV) is the primary metadata resource that describes an Operator.   
2. You can think of a CSV as analogous to a Linux package, such as a Red Hat Package Manager (RPM) file.  
 
2. Each CSV represents a version of an Operator and contains the following.  
    a. General metadata about the Operator, including its name, version, description, and icon.  
    b. Operator installation information, describing the deployments that are created and the permissions that are required.  
    c. The CRDs that are owned by the Operator as well as references to any CRDs the Operator is dependent on.  
    d. Annotations on the CRD fields to provide hints to users on how to properly specify values for the fields.  
   
### Operator Lifecycle Manager  
1. operators are monitor, maintain, recover, and upgrade the software they deploy.  
2. Operator manages its operand.    
Q1. what manages an Operator?     
a. Operator Lifecycle Manager takes the Operator pattern one level up the stack.  
b. it’s an Operator that acquires, deploys, and manages Operators on a Kubernetes cluster.   
c. OLM extends Kubernetes by way of custom resources and custom controllers so that Operators can be managed with   
Kubernetes tools, in terms of the Kubernetes API.   

### how operators Lifecycle Manager  work     
1. OLM defines a schema for Operator metadata, called the Cluster Service Version (CSV), for describing an Operator and       
its dependencies.   
2. Operators with a CSV can be listed as entries in a catalog available to OLM running on a Kubernetes cluster.    
3. Based on the description and parameters an Operator provides in its CSV  OLM can manage the Operator over its lifecycle.   
4. Users subscribe to an Operator from the catalog to tell OLM to provision and manage a desired Operator.   
5. Then Operator is turn, provisions and manages its application or service on the cluster.       

### CatalogSource    
1. A CatalogSource contains information for accessing a repository of Operators.   
2. OLM provides a utility API named packagemanifests for querying catalog sources.  
3. It provides a list of Operators and the catalogs in which they are found.   

### Subscription  
1. End users create a subscription to install and update the Operators that OLM provides.   
``` 
example  
To continue with the earlier analogy to Linux packages, a subscription is equivalent to a command that installs a package.  
````   
### InstallPlan  
1. A subscription creates an InstallPlan.  
2. It describes the full list of resources that OLM will create to satisfy the CSV’s resource requirements.   
3. Because users do not need to explicitly interact with these resources.   
### OperatorGroup  
1. End users control Operator multitenancy through an OperatorGroup.   
2. Operator belonging to an OperatorGroup will not react to custom resource changes.  
3. OperatorGroups for fine-grained control for a set namespace there are two way.  
a. To scope an Operator to a single namespace 
b. To allow an Operator to run globally across all namespaces  

Q1. relationship between a CSV and Operator.?  
