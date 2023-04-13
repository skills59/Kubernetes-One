# Kubernetes-One
Simple kubernetes exercise deploying a fullstack sringboot react application to kubernets using minikube and kubectl 

# What you need to do this excercise
 ## -Installations: Docker + Minikibe
 once you have a local cluster up and running with minikube on the local machine,
 then kubectl can be used to interact with the clusters from the local machine.

# Steps to take before the excercise 
- make sure you have your fullstatck alication built and ready on vscode 
- Push project to github
- build or create an image for the aplcation using docker
- push to dockerhub

## Once you have your image on dockerhub we can now start the excercise using minikube and kubectl 
1 we need to create 2 nodes using the script 
- "minikube start --nodes=2"
- This creates a master node running the control plane and the second node which is the worker node
- this can be confirmed using the script
- "kubectl get nodes"

2- check all Pods
- "kubectl get pods"
- this displays all of the pods that make up the control plane

3- head on to your vscode create a project file called kubernetes.

4- create a YAML file called deployment 
- "deployment.yml"


5- in the deployment template 
  - create a deployment,
  - state the number of replicas which = 2, 
  - create a service
  - include and pull the fullstack aplication image previously pushed to dockerhub on the template 
  - eg i used this image : amigoscode/kubernetes:springboot-react-fullstack-v1
  - create your listening port = 80
  - target port should be =8080
  - increased the memory size to = 512Mi
  - expose the service to a NodePort or LoadBalancer but ffor this project i used a NodePort 
  
# Template Sample

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: 
        resources:
          limits:
            memory: "512Mi"
            cpu: "500m"
        ports:
        - containerPort: 8080

---

apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 8080

---


6- now deploy the template use the script 
- "kubectl apply -f deployment.yml"


7-confirm using the following scripts 
 - "kubectl get deployments"
 - "kubectl get pods"
 - "kubectl get services or svc"
 
8-  in order to access the service or alication deployed, make use of the following script
  - "minikube service {service name}"
- it automatically opens up on your web browser, if it doesnt it dislays the url to find the application 
  - e.g : 127.1.1.0:2324

9- Finally to view this service or deployment on a dashboard locally you can make use of the script
  - "minikube dashboard --url"












 
 
 


