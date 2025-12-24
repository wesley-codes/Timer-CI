# Timer App - DevOps Project

A simple Flask web application that displays the current time, fully containerized and deployed using modern DevOps practices including Docker, Kubernetes, Helm, CI/CD, and GitOps.

## 🚀 Features

- **Flask Web Application**: Displays the current time in `YYYY-MM-DD HH:MM:SS` format
- **Docker Containerization**: Lightweight Python 3.9-slim based container
- **Kubernetes Deployment**: Helm chart for easy deployment and management
- **CI/CD Pipeline**: Automated build, push, and deployment via GitHub Actions
- **GitOps**: ArgoCD for continuous deployment and synchronization
- **Infrastructure as Code**: Terraform for provisioning Kubernetes infrastructure

## 📋 Prerequisites

- Docker
- Kubernetes cluster (or Minikube)
- kubectl
- Helm 3.x
- Terraform (for infrastructure setup)
- GitHub account with repository access
- Docker Hub account (for image registry)

## 🏗️ Architecture

```
┌─────────────┐
│   GitHub    │
│  Repository │
└──────┬──────┘
       │
       ├──> GitHub Actions (CI/CD)
       │    ├──> Build Docker Image
       │    ├──> Push to Docker Hub
       │    └──> Update Helm Chart
       │
       └──> ArgoCD (GitOps)
            └──> Deploy to Kubernetes
                 └──> Timer App Pod
```

## 📁 Project Structure

```
Time-DevOPs/
├── app.py                    # Flask application
├── dockerfile                # Docker image definition
├── argocd-app.yaml          # ArgoCD application manifest
├── .github/
│   └── workflows/
│       └── ci.yaml          # GitHub Actions CI/CD pipeline
├── terraform-configs/       # Infrastructure as Code
│   ├── main.tf              # Minikube cluster configuration
│   ├── provider.tf          # Terraform providers
│   ├── backend.tf           # Terraform backend configuration
│   └── argocd.tf            # ArgoCD Helm release
└── timerapp/                # Helm chart
    ├── Chart.yaml
    ├── values.yaml          # Helm values
    └── templates/
        └── deployment.yaml  # Kubernetes deployment template
```

## 🚀 Getting Started

### Local Development

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Time-DevOPs
   ```

2. **Run the application locally**
   ```bash
   python app.py
   ```
   The app will be available at `http://localhost:5000`

### Docker

1. **Build the Docker image**
   ```bash
   docker build -t timerapp:latest .
   ```

2. **Run the container**
   ```bash
   docker run -p 5000:5000 timerapp:latest
   ```

3. **Access the application**
   ```bash
   curl http://localhost:5000
   ```

### Kubernetes Deployment

#### Using Terraform (Infrastructure Setup)

1. **Initialize Terraform**
   ```bash
   cd terraform-configs
   terraform init
   ```

2. **Create Minikube cluster**
   ```bash
   terraform apply
   ```

3. **Deploy ArgoCD**
   ```bash
   terraform apply
   ```
   This will install ArgoCD in the `argocd` namespace.

#### Using Helm

1. **Install the Helm chart**
   ```bash
   helm install timerapp ./timerapp
   ```

2. **Check deployment status**
   ```bash
   kubectl get pods
   kubectl get services
   ```

3. **Port forward to access the application**
   ```bash
   kubectl port-forward <pod-name> 8081:5000
   ```
   Then access at `http://localhost:8081`

#### Using ArgoCD (GitOps)

1. **Get ArgoCD admin password**
   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
   ```

2. **Port forward ArgoCD UI**
   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443
   ```

3. **Apply ArgoCD Application**
   ```bash
   kubectl apply -f argocd-app.yaml
   ```

4. **Access ArgoCD UI**
   - URL: `https://localhost:8080`
   - Username: `admin`
   - Password: (from step 1)

ArgoCD will automatically sync and deploy the application from the Git repository.



### CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/ci.yaml`) automatically:
1. Builds Docker image tagged with Git SHA
2. Pushes to Docker Hub
3. Updates Helm chart with new image tag
4. Commits and pushes changes back to repository

**Required GitHub Secrets:**
- `DOCKERHUB_USERNAME`: Docker Hub username
- `DOCKERHUB_TOKEN`: Docker Hub access token

### ArgoCD Application

The ArgoCD application (`argocd-app.yaml`) is configured with:
- **Source**: Git repository with Helm chart
- **Destination**: Kubernetes cluster
- **Sync Policy**: Automated with prune and self-heal enabled




## 📝 API

### Endpoints

- `GET /` - Returns the current time in `YYYY-MM-DD HH:MM:SS` format

**Example Response:**
```
The Current time of the day : 2024-12-24 10:30:45
```

## 🛠️ Technologies Used

- **Python 3.9**: Application runtime
- **Flask**: Web framework
- **Docker**: Containerization
- **Kubernetes**: Container orchestration
- **Helm**: Package manager for Kubernetes
- **GitHub Actions**: CI/CD pipeline
- **ArgoCD**: GitOps continuous delivery
- **Terraform**: Infrastructure as Code
- **Minikube**: Local Kubernetes cluster

## 📄 License

This project is part of a DevOps learning exercise.

## 👤 Author

**wesley-codes**
- Email: ezemikey12@gmail.com
- GitHub: [wesley-codes](https://github.com/wesley-codes)

## 🤝 Contributing

This is a personal DevOps project. Feel free to fork and modify for your own learning purposes.

---

**Note**: This application is designed for educational and demonstration purposes to showcase modern DevOps practices and tooling.

