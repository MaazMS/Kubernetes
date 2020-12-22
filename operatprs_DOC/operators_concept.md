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


