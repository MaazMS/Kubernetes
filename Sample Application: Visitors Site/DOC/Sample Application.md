### Sample Application: Visitors Site  
1. Container-based architectures are often made up of multiple services, each requiring their own configuration and   
installation process.    
2. Maintaining these types of applications, including the individual components and their interactions, is a time-consuming  
and error-prone process.   
3. Operators are designed to reduce the difficulty in this process.     
4. We’ll take a look at the application architecture and how to run the site, as well as the process of installing it through  
 traditional Kubernetes manifests.   
5.  we’ll create Operators to deploy this application using each of the approaches provided by the Operator SDK   
(Helm, Ansible, and Go), and explore the benefits and drawbacks of each.  
### Application Overview   
1. The Visitors Site tracks information about each request to its home page.  
2. Each time the page is refreshed, an entry is stored with details about the client, backend server,and timestamp.  
* The Visitors Site is a traditional, three tier application, consisting of.  
1. A web frontend, implemented in React.  
2. A REST API, implemented in Python using the Django framework.  
3. A database, using MySQL.  
**Each of these components is deployed as a separate container**   
### flow of Application   
1. users interacting with the web interface, which itself makes calls to the backend REST API.   
2. The data submitted to the REST API is persisted in a MySQL database.   
**Note** That the database does not connect to a persistent volume and stores its data ephemerally.     

### Installation with Manifests    
1. Visitors Site requires two Kubernetes resources    
* Deployment  
    1. create the containers, including the image name, exposed ports, and specific configuration for a single deployment.    
 * Service  
    1. 
     
