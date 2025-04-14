🚀 TASK - Build a Kubernetes Cluster Locally with Minikube

✔️ This project demonstrates how to build a Kubernetes cluster locally using Minikube and deploy a simple NGINX application.

🛠 Tools Used

Minikube
kubectl
Docker
EC2 Ubuntu Instance
✅ Task 5: Build a Kubernetes Cluster Locally with Minikube
Objective: Deploy and manage an application inside a Kubernetes cluster.
Tools Used: Kind (alternative to Minikube), kubectl, Docker, Ubuntu EC2 (Free Tier)

🧱 Step-by-Step Summary:
✅ 1. Cluster Setup
Installed Docker and kubectl on Ubuntu EC2.

Since Minikube required more RAM than available, switched to Kind, a lightweight Kubernetes cluster for local testing.

Created a single-node cluster using Kind.

Verified with:

bash
Copy
Edit
kubectl get nodes

✅ 2. Deployment & Service YAML

📄 deployment.yaml
yaml
Copy
Edit
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
        
📄 service.yaml
yaml
Copy
Edit
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30080
      
✅ 3. Commands Executed
bash
Copy
Edit
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods
kubectl get services
kubectl port-forward service/nginx-service 8080:80
curl localhost:8080
kubectl scale deployment nginx-deployment --replicas=4
kubectl describe pod <pod-name>
kubectl logs <pod-name>




🏁 Result:
✅ Successfully deployed and exposed an NGINX app.

✅ Scaled deployment to 4 pods.

✅ Verified functionality with port-forward and curl.




🙌 Author GitHub: @kavya9864
