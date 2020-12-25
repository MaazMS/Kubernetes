### Backend     
1. backend needs both a deployment and a service.  
2. This isn’t an unreasonable requirement, it falls on the user to ensure that the values are consistent across both resources.  
3. A single error could result in the backend not being able to communicate with the database.  
``` 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: visitors-backend
spec:
  replicas: 1 # point 1
  selector:
    matchLabels:
      app: visitors
      tier: backend
  template:
    metadata:
      labels:
        app: visitors
        tier: backend
    spec:
      containers:
        - name: visitors-backend
          image: "jdob/visitors-service:1.0.0"
          imagePullPolicy: Always
          ports:
            - name: visitors
              containerPort: 8000
          env:
            - name: MYSQL_DATABASE # point 2
              value: visitors_db
            - name: MYSQL_SERVICE_HOST # point 3
              value: mysql-service
            - name: MYSQL_USERNAME
              valueFrom:
                secretKeyRef:
                  name: mysql-auth # point 4
                  key: username
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-auth # point 5  
                  key: password
```  
1. Each deployment configuration includes the number of containers it should spawn.  
2. values must be manually checked to ensure they match up with the values set on the MySQL deployment, Otherwise, the   
backend will not be able to establish a connection to the database.  
3. This value tells the backend where to find the database and must match the name of the MySQL service created previously.    
4. The secret provides the authentication credentials for the database.    
* use this command   
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f backend.yaml 
deployment.apps/visitors-backend created
```

* The service manifest looks similar to the one you created for the database.  
``` 
apiVersion: v1
kind: Service
metadata:
  name: visitors-backend-service
  labels:
    app: visitors
    tier: backend
spec:
  type: NodePort
  ports:
    - port: 8000  # point 1
      targetPort: 8000
      nodePort: 30685  # point 2
      protocol: TCP
  selector:
    app: visitors
    tier: backend
```
1. port referenced in the service definition must match up with that exposed by the deployment.  
2. the backend is configured to run through port 30685 on the same IP as Minikube. The frontend uses this port when   
making backend calls for data.     
* use this command       
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f backend.yaml 
deployment.apps/visitors-backend unchanged
service/visitors-backend-service created
``` 