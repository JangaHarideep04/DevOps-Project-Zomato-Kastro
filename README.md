# 📦 DevOps Project: Zomato Clone – CI/CD with Jenkins, Docker, Kubernetes, ArgoCD, and Terraform

This project demonstrates a full-stack DevOps pipeline using modern tools and practices. It includes CI/CD, containerization, infrastructure as code, code quality checks, and real-time monitoring.

---

## 📌 Project Overview

- **Frontend App:** Zomato Clone (Node.js)
- **CI/CD Tool:** Jenkins
- **Containerization:** Docker
- **Orchestration:** Kubernetes (EKS)
- **Infrastructure as Code:** Terraform
- **GitOps:** ArgoCD
- **Code Quality:** SonarQube, OWASP Dependency Check, Trivy
- **Container Security:** Docker Scout
- **Monitoring:** Prometheus + Grafana
- **Email Alerts:** Jenkins Email Ext Plugin with Gmail SMTP

---

## 📁 Project Structure

```
DevOps-Project-Zomato-Kastro/
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── jenkins-pipeline.groovy
├── sonar-project.properties
├── trivy.txt (generated)
├── terraform/
│   ├── main.tf
│   └── ...
└── README.md
```

---

## 🔧 Tools Used

| Tool            | Purpose                              |
|-----------------|--------------------------------------|
| **Terraform**   | Provision VPC, EKS, EC2, IAM         |
| **Jenkins**     | CI/CD pipeline automation            |
| **Docker**      | App containerization                 |
| **Kubernetes**  | Container orchestration (EKS)        |
| **ArgoCD**      | GitOps-based deployment              |
| **SonarQube**   | Code quality and static analysis     |
| **OWASP Check** | Dependency scanning for vulnerabilities |
| **Trivy**       | File system scanning for security    |
| **Docker Scout**| Container security scan              |
| **Prometheus**  | Metrics collection                   |
| **Grafana**     | Visualization of metrics             |
| **Gmail SMTP**  | Email notifications                  |

---

## 🌐 Architecture Diagram

> You can generate and add a diagram using [draw.io](https://draw.io/) or [Lucidchart].

High-level overview:

- Terraform provisions AWS infrastructure (VPC, EKS, EC2)
- Jenkins installed in EC2 (private subnet) with NAT Gateway
- Node.js app is built & scanned in Jenkins
- Docker image pushed to DockerHub
- Kubernetes manifests managed in GitHub → auto-synced with ArgoCD
- Monitoring with Prometheus & Grafana
- Email alerts sent post-build with Trivy results

---

## 🚀 CI/CD Workflow (Jenkins Pipeline)

### ✅ Stages:

1. **Clean Workspace**
2. **Checkout Code**
3. **SonarQube Analysis**
4. **Code Quality Gate**
5. **Install Dependencies**
6. **OWASP Dependency Check**
7. **Trivy Scan**
8. **Docker Build**
9. **Push to DockerHub**
10. **Docker Scout Scan**
11. **Deploy Container**
12. **Email Notification with Attachment (Trivy)**

### 📧 Email Format:
HTML-based mail with:
- Project Name
- Build Number
- Build URL
- Trivy Scan as attachment

---

## ⚙️ Key Jenkinsfile Snippet

```groovy
post {
  always {
    emailext attachLog: true,
      subject: "'${currentBuild.result}'",
      body: "...HTML content...",
      to: 'jangaharidee@gmail.com',
      mimeType: 'text/html',
      attachmentsPattern: 'trivy.txt'
  }
}
```

---

## 🛡️ Security Scans

| Tool        | Scan Type                 |
|-------------|---------------------------|
| SonarQube   | Static Code Analysis      |
| Trivy       | File System Vulnerability |
| OWASP Check | Dependency Vulnerability  |
| Docker Scout| Container Image Security  |

---

## 🚢 Kubernetes Deployment (ArgoCD)

### Sample `service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: zomato
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 3000
  selector:
    app: LoadBalancer
```

### ArgoCD Sync Output:

```
kubectl get applications -n argocd
NAME     SYNC STATUS   HEALTH STATUS
zomoto   Synced        Healthy
```

---

## 📊 Monitoring & Alerts

- Prometheus scrapes metrics from Jenkins and Node app
- Grafana dashboards visualize metrics
- Email alerts triggered on every Jenkins build

---

## 🧱 Infrastructure (Terraform)

Terraform modules include:

- VPC with public/private subnets
- NAT Gateway and Internet Gateway
- EKS Cluster + Worker Nodes
- EC2 instance for Jenkins

---

## 🔐 Email Notification Setup

### Gmail SMTP Settings (Jenkins → Manage Jenkins → Email Ext Plugin):

- SMTP Server: `smtp.gmail.com`
- Port: `465`
- SSL: Enabled
- Auth: Enabled
- User: `jangaharidee@gmail.com`
- Password: **App Password**
- Default Recipients: `jangaharidee@gmail.com`
- Content Type: `HTML (text/html)`

---

## 📦 DockerHub

Docker images pushed with tags:

```
harideep0412/zomato-<build_number>:latest
```

---

## 💡 Future Enhancements

- Add Helm chart for Zomato app
- Setup Slack notifications
- Use GitHub Actions for CI
- Enable RBAC for Jenkins & ArgoCD
- Automate Prometheus + Grafana using Helm

---

## 🙋‍♂️ Author

**Harideep Janga**  
DevOps Enthusiast | AWS | Jenkins | Kubernetes  
📧 jangaharidee@gmail.com  
🔗 [GitHub](https://github.com/JangaHarideep04)
