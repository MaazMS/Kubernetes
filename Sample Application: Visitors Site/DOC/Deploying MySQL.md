### Deploying MySQL  
1. The secret must be created before the database is deployed.  
```  
apiVersion: v1
kind: Secret
metadata:
  name: mysql-auth
type: Opaque
stringData:
  username: visitors-user
  password: visitors-pass
```  
* Explain  
1. When the database and backend deployments use the secret, it is referred to by this name `name: mysql-auth`   
2. For simplicity in this example, the username and password are defaulted to testing values. `username` and `password`    

* use this command   
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f database.yaml 
secret/mysql-auth created
``` 
* Once the secret is in place following manifest to deploy a MySQL instance into Kubernetes.   
```  
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql # point 1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: visitors
      tier: mysql
  template:
    metadata:
      labels:
        app: visitors
        tier: mysql
    spec:
      containers:
        - name: visitors-mysql
          image: "mysql:5.7"  # point 2
          imagePullPolicy: Always
          ports:
            - name: mysql
              containerPort: 3306  # point 3
              protocol: TCP
          env:   # point 4
            - name: MYSQL_ROOT_PASSWORD
              value: password
            - name: MYSQL_DATABASE
              value: visitors_db
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-auth  # point 5
                  key: username
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-auth  # point 5
                  key: password
```   
1. The deployment name must be unique to the namespace in which it is deployed.   
2. The deployment requires the details of the image to deploy, including its name and hosting repository.   
3. Users must be aware of each port that the image exposes, and must explicitly reference them.   
4. The values used to configure the containers for this specific deployment are passed as environment variables.  
5. The secret provides the values for the database authentication credentials.  
6. the value of the container port, as well as each of the environment variables, as other manifests use these values.    
* use this command     
```  
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f database.yaml 
secret/mysql-auth configured
deployment.apps/mysql created
``` 
1. The deployment causes the creation of the MySQL container.  
2. however, it does not provide any `ingress` configuration on how to access it.    
3. For that, we will need a service.  
``` 
apiVersion: v1
kind: Service
metadata:
  name: mysql-service # point 1
  labels:
    app: visitors
    tier: mysql
spec:
  clusterIP: None
  ports:
    - port: 3306 # point 2
  selector:
    app: visitors
    tier: mysql
```
1. As with deployments, service names must be unique in a given namespace.This will also apply to the deployment and   
services for the backend and frontend components.   
2. The service maps to a port exposed by a deployment, so this value must be the same as in the ports section of the deployment.     
* use this command    
```` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f database.yaml 
secret/mysql-auth configured
deployment.apps/mysql unchanged
service/mysql-service created
````
