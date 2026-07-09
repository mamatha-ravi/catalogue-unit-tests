# Catalogue Service — Unit Tests with CI/CD Pipeline

RoboShop catalogue microservice with unit tests,
Docker containerisation, SonarQube code quality
scanning, and Jenkins CI/CD pipeline integration.

---

## What is in This Repo

| File/Folder | Purpose |
|-------------|---------|
| `Jenkinsfile` | CI/CD pipeline using Jenkins Shared Library |
| `Dockerfile` | Container image build configuration |
| `sonar-project.properties` | SonarQube code quality configuration |
| `package.json` | Node.js dependencies and scripts |
| `server.js` | Catalogue microservice application |
| `test/` | Unit test suite |
| `db/` | Database schema and seed data |

---

## CI/CD Pipeline

This repo uses the
[jenkins-shared-library](https://github.com/mamatha-ravi/jenkins-shared-library)
for its pipeline via `nodeJSEKSPipeline()`.

```groovy
def configMap = [
  project:   "roboshop",
  component: "catalogue"
]

nodeJSEKSPipeline(configMap)
```

### Pipeline Stages
Code Push to GitHub
↓
Jenkins detects branch
↓
Calls nodeJSEKSPipeline from Shared Library
↓
Install dependencies — npm install
↓
Run unit tests — npm test
↓
SonarQube code quality scan
↓
Docker build and tag
↓
Push to AWS ECR
↓
Deploy to Kubernetes (EKS)
---

## How to Run Locally

```bash
# Install dependencies
npm install

# Run unit tests
npm test

# Start the service
node server.js
```

## How to Build Docker Image

```bash
docker build -t catalogue:latest .
docker run -p 8080:8080 catalogue:latest
```

---

## Tech Stack

| Category | Technology |
|----------|------------|
| Runtime | Node.js |
| Testing | Mocha / Jest |
| CI/CD | Jenkins + Shared Library |
| Container | Docker |
| Code Quality | SonarQube |
| Registry | AWS ECR |
| Orchestration | Kubernetes on EKS |

---

## Related Repos

| Repo | Description |
|------|-------------|
| [jenkins-shared-library](https://github.com/mamatha-ravi/jenkins-shared-library) | Shared pipeline library used by this repo |
| [roboshop-infra-dev](https://github.com/mamatha-ravi/roboshop-infra-dev) | Full RoboShop AWS infrastructure |
| [terraform-aws-eks](https://github.com/mamatha-ravi/terraform-aws-eks) | EKS cluster this service deploys to |

---

## Author

Mamatha Ravipati
📍 Hyderabad, India
📧 mamata.r@gmail.com
🔗 [github.com/mamatha-ravi](https://github.com/mamatha-ravi)
