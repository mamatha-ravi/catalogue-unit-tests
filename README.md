# Catalogue Service — Unit Tests with CI/CD
 
RoboShop catalogue microservice with unit tests, Docker build,
SonarQube quality scan, and Jenkins CI/CD pipeline to EKS.
 
---
 
## Files
 
| File/Folder | Purpose |
|-------------|---------|
| Jenkinsfile | CI/CD pipeline via Jenkins Shared Library |
| Dockerfile | Container image build |
| sonar-project.properties | SonarQube configuration |
| test/ | Unit test suite |
| db/ | Database schema and seed data |
 
---
 
## Pipeline
 
Uses [jenkins-shared-library](https://github.com/mamatha-ravi/jenkins-shared-library):
 
```groovy
@Library('jenkins-shared-library') _
def configMap = [project: "roboshop", component: "catalogue"]
nodeJSEKSPipeline(configMap)
```
 
Stages: npm install → tests → SonarQube → Docker build → Trivy → ECR → Helm deploy to EKS
 
---
 
## Branch Protection
 
main branch is protected:
- All scans must pass before merge
- PR required — no direct push to main
 
---
 
## How to Run
 
```bash
npm install
npm test
 docker build -t ${acc_id}.dkr.ecr.${region}.amazonaws.com/${project}/${component}:${appVersion} .
 helm upgrade --install ${component} -f values-prod.yaml -n ${project}-prod --atomic --wait --timeout=5m .
```
 
---
 
## Tech Stack
 
Node.js · Docker · Jenkins · SonarQube · Trivy · AWS ECR · Kubernetes .Helm
 
---
 
## Author
 
Mamatha Ravipati
📍 Hyderabad, India | 📧 mamata.r@gmail.com
🔗 github.com/mamatha-ravi
