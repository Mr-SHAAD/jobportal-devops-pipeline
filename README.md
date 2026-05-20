# 🚀 JobPortal DevOps Pipeline

<div align="center">

![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![AWS ECR](https://img.shields.io/badge/AWS%20ECR-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)
![Security](https://img.shields.io/badge/Security-Trivy%20Scan-1904DA?style=for-the-badge&logo=aquasecurity&logoColor=white)

**A production-grade DevSecOps CI/CD pipeline for a Django REST API**  
*Auto-build → Security Scan → Push to AWS ECR on every commit*

</div>

---

## 🏗️ Pipeline Architecture

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│   Developer pushes code                                 │
│         │                                               │
│         ▼                                               │
│   ┌─────────────┐                                       │
│   │   GitHub    │  triggers automatically               │
│   │   Actions   │─────────────────────┐                 │
│   └─────────────┘                     │                 │
│                                       ▼                 │
│                             ┌──────────────────┐        │
│                             │  Docker Image    │        │
│                             │     Build        │        │
│                             └────────┬─────────┘        │
│                                      │                  │
│                                      ▼                  │
│                             ┌──────────────────┐        │
│                             │  Trivy Security  │        │
│                             │  Vulnerability   │        │
│                             │     Scan  🔍     │        │
│                             └────────┬─────────┘        │
│                                      │                  │
│                                      ▼                  │
│                             ┌──────────────────┐        │
│                             │   AWS ECR Push   │        │
│                             │   ☁️ Image Live  │        │
│                             └──────────────────┘        │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Django 5.2, Django REST Framework |
| **Database** | PostgreSQL 15 |
| **Cache** | Redis 7 |
| **Containerization** | Docker, Docker Compose |
| **CI/CD** | GitHub Actions |
| **Security** | Trivy Vulnerability Scanner |
| **Registry** | AWS ECR (Elastic Container Registry) |
| **Server** | Gunicorn (Production WSGI) |

---

## ✨ Key Features

- 🔄 **Auto-triggered pipeline** — Every push to `main` runs the full pipeline
- 🐳 **Multi-service Docker** — Django + PostgreSQL + Redis via Docker Compose
- 🔐 **DevSecOps** — Trivy scans Docker image for vulnerabilities before push
- ☁️ **AWS ECR** — Production Docker image stored in private AWS registry
- ⚡ **Fast builds** — Cached Docker layers for optimized build time
- 🔒 **Zero secrets exposed** — All credentials via GitHub Secrets

---

## 🚀 Run Locally

### Prerequisites
- Docker & Docker Compose installed
- Git

### Steps

```bash
# Clone the repo
git clone https://github.com/Mr-SHAAD/jobportal-devops-pipeline
cd jobportal-devops-pipeline

# Setup environment
cp .env.example .env
# Edit .env with your values

# Start all services
docker-compose up --build
```

**App live at:** `http://localhost:8000`

**Services running:**
- Django API → `localhost:8000`
- PostgreSQL → `localhost:5433`
- Redis → `localhost:6379`

---

## 📋 Pipeline Steps (cicd.yml)

```yaml
1. Checkout Code          ← Pull latest code
2. Configure AWS Creds    ← Authenticate with AWS
3. Login to ECR           ← Connect to registry
4. Build Docker Image     ← Build production image
5. Trivy Security Scan    ← Scan for vulnerabilities
6. Push to AWS ECR        ← Store image in cloud
```

---

## 🔐 Environment Variables

Create a `.env` file in root:

```env
SECRET_KEY=your-django-secret-key
DEBUG=False
DB_NAME=jobportal
DB_USER=postgres
DB_PASSWORD=your-password
DB_HOST=db
DB_PORT=5432
REDIS_URL=redis://redis:6379/1
```

**GitHub Secrets required:**
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`

---

## 📁 Project Structure

```
jobportal-devops-pipeline/
├── 📄 Dockerfile                    # Production Docker image
├── 📄 docker-compose.yml            # Multi-service setup
├── 📄 requirements.txt              # Python dependencies
├── 📄 .env.example                  # Environment template
├── 📁 .github/
│   └── 📁 workflows/
│       └── 📄 cicd.yml              # CI/CD pipeline
└── 📄 README.md
```

---

## 🔄 CI/CD Pipeline Status

| Step | Status |
|------|--------|
| Docker Build | ✅ Passing |
| Trivy Scan | ✅ Passing |
| ECR Push | ✅ Passing |

---

## 👨‍💻 Author

**Mohammad Shaad**  
[![GitHub](https://img.shields.io/badge/GitHub-Mr--SHAAD-181717?style=flat&logo=github)](https://github.com/Mr-SHAAD)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mohammad%20Shaad-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/mohammadshaad)

---

<div align="center">
<sub>Built with ❤️ — Django • Docker • GitHub Actions • AWS ECR</sub>
</div>
