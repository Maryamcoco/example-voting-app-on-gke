# 🗳️ Example Voting App on GKE

This project demonstrates the deployment of the **Example Voting App** on **Google Kubernetes Engine (GKE)** using **Docker**, **Kubernetes manifests**, and **Ingress** for external access.  

The application is a microservices-based voting system that allows users to vote between two options (e.g., Cats 🐱 vs Dogs 🐶) and view real-time results.  
It was originally created by Docker and adapted here to showcase DevOps and Kubernetes deployment skills — from local testing to cloud-based orchestration.

---

## 📝 Project Description

This project highlights:
- Containerization and local testing with **Docker Compose**
- **Cluster creation** and deployment on **Google Kubernetes Engine (GKE)**
- Use of **Kubernetes manifests** for defining Deployments, Services, and Ingress
- Exposure of applications via **Ingress Controller**
- Port-forward testing and namespace isolation

It demonstrates practical DevOps workflow for running a multi-service app on Kubernetes using Google Cloud infrastructure.

---

## 🧩 Project Structure

├── docker-compose.yml # Local setup for testing all services together
├── k8s-specifications/
│ ├── namespace.yaml
│ ├── vote-deployment.yaml
│ ├── vote-service.yaml
│ ├── result-deployment.yaml
│ ├── result-service.yaml
│ ├── redis-deployment.yaml
│ ├── postgres-deployment.yaml
│ ├── worker-deployment.yaml
│ └── ingress.yaml
└── README.md


---

## ⚙️ Technologies Used

- **Docker** – Containerization  
- **Docker Compose** – Local testing and service linking  
- **Kubernetes (kubectl)** – Deployment and cluster management  
- **Google Kubernetes Engine (GKE)** – Managed Kubernetes cluster  
- **Ingress Controller** – External routing and load balancing  
- **Redis & Postgres** – Data storage for votes and results  

---

## 🚀 Deployment Workflow

### 🧱 1. Local Testing with Docker Compose

Run all services locally to confirm functionality:

```bash
docker compose up -d
```
Then open:

Vote app → http://localhost:8080

Result app → http://localhost:8081

### ☁️ 2. Create a GKE Cluster

Provision your Kubernetes cluster on Google Cloud:

gcloud container clusters create voting-cluster \
  --region us-central1 \
  --num-nodes 1 \
  --machine-type e2-standard-4


Connect your terminal to the cluster:

gcloud container clusters get-credentials voting-cluster --region us-central1

### 🧩 3. Deploy the Application
Create Namespace


Apply Kubernetes Manifests
kubectl apply -f k8s-manifests/


Check if pods are running:

kubectl get pods -n voting-app

🔁 4. Test via Port Forwarding

Before setting up ingress, you can access the app locally using port forwarding:

kubectl port-forward svc/vote 8080:80 -n voting-app
kubectl port-forward svc/result 8081:80 -n voting-app


Access locally:

Vote app → http://localhost:8080

Result app → http://localhost:8081

🌐 5. Expose via Ingress

After confirming your services run correctly, apply the ingress configuration:

kubectl apply -f k8s-specifications/ingress.yaml


Get the external IP:

kubectl get ingress -n voting-app


Access your app using the Ingress external IP or custom domain.
## GIF
![GIF](https://github.com/Maryamcoco/example-voting-app-on-gke/blob/main/voting%20gif.gif)

## 📸 Screenshots
![Vote App](https://github.com/Maryamcoco/example-voting-app-on-gke/blob/main/Screenshot%202025-10-22%20161428.png)

Result App
![Result App](
	

(Replace with your actual screenshots — optimized for web display.)

## 💡 Lessons Learned

- How to create and connect to a GKE cluster

- The difference between Docker Compose networking and Kubernetes Service discovery

- Steps to expose applications externally using Ingress

- Importance of testing locally before deploying to the cloud

- Understanding namespace isolation and service communication

## 🧰 Future Enhancements

- Add CI/CD pipeline using Jenkins or GitHub Actions

- Implement Prometheus + Grafana monitoring

- Deploy via Helm chart for easier versioning and configuration

- Integrate Datadog or New Relic for advanced observability


## 👩🏽‍💻 Author

**Maryam Abdulrauf**
*Junior DevOps Engineer | Cloud & Automation Enthusiast*

📧 [abdulraufmaryam15@gmail.com]

🏷️ License

This project is licensed under the MIT License


