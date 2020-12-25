### Frontend   
1. frontend is in a similar position as the backend.  
2. user to manually verify that these values are consistent in both locations.(Frontend and backend)    
```  
apiVersion: apps/v1
kind: Deployment
metadata:
  name: visitors-frontend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: visitors
      tier: frontend
  template:
    metadata:
      labels:
        app: visitors
        tier: frontend
    spec:
      containers:
        - name: visitors-frontend
          image: "jdob/visitors-webui:1.0.0"
          imagePullPolicy: Always
          ports:
            - name: visitors
              containerPort: 3000
          env:
            - name: REACT_APP_TITLE  # point 1 
              value: "Visitors Dashboard"
``` 
1. To make the Visitors Site application more interesting, you can override the home page title through an environment variable.     
* use this command      
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f frontend.yaml 
deployment.apps/visitors-frontend created
```  
* The service manifest looks similar to the one you created for the backend.     
``` 
apiVersion: v1
kind: Service
metadata:
  name: visitors-frontend-service
  labels:
    app: visitors
    tier: frontend
spec:
  type: NodePort
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30686  # point 1 
      protocol: TCP
  selector:
    app: visitors
    tier: frontend
```
1. The frontend service looks very similar to the backend service, with the notable difference that it runs on port 30686.   
* use this command   
``` 
maaz@maaz-Lenovo-G50-70:~/github/Kubernetes/Sample Application: Visitors Site$ kubectl apply -f frontend.yaml 
deployment.apps/visitors-frontend unchanged
service/visitors-frontend-service created
``` 
