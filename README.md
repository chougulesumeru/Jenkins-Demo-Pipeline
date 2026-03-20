# Jenkins End-to-End DevOps Pipeline 🚀

A complete **declarative Jenkins pipeline** that covers the full CI/CD lifecycle for a modern application:

Git → Code Quality (SonarQube) → Build → Docker → Terraform (Infra) → Kubernetes Deploy

One single `Jenkinsfile` that takes your code from commit → production (safely storing all secrets in Jenkins credentials — never in git!).

## ✨ Pipeline Overview

This pipeline automates everything a typical DevOps project needs in 2025–2026:

- Clean start
- Pull code from Git
- Static code analysis + quality gate
- Build app
- Create & push Docker image
- Provision/update infrastructure with Terraform
- Deploy to Kubernetes (EKS example)
- Nice success/failure notifications

## 📋 Pipeline Breakdown (Line-by-Line – Super Simple)

<details>
<summary>Click to expand full explanation with emojis</summary>

| Step | Emoji | What it does (in plain English) | Example analogy |
|------|-------|----------------------------------|-----------------|
| `pipeline {` | 🧾 | Start of the entire automation recipe. Everything inside runs when code is pushed. | Your full cooking recipe card |
| `agent any` | 🖥️ | Run on any available Jenkins machine (server or agent). | "Use any computer in the office" |
| `tools { nodejs 'node20' }` | 🔧 | Use the Node.js version you named 'node20' in Jenkins tools. (Change to Maven for Java) | Picking the right screwdriver from your toolbox |
| `environment { ... }` | 🏷️ | Create reusable variables (like Docker image name with build number) | Labeling your lunchbox with today's date |
| `stages {` | 🏗️ | All the real work lives here — one stage at a time | The chapters of your recipe |
| `stage('Clean Workspace')` | 🧹 | Delete old files so we start fresh every time | Wiping your desk clean before homework |
| `stage('Git Checkout')` | 📥 | Pull latest code from GitHub using your secret credential (`git-creds`) | "Hey Jenkins, fetch my code with my secret key!" |
| `stage('SonarQube Analysis')` | 🔍 | Scan code for bugs, security issues, code smells → send to SonarQube dashboard | Teacher checking homework for mistakes |
| `stage('Quality Gate')` | ✅❌ | Wait for SonarQube verdict. Red quality gate? → pipeline stops! | Teacher says: "Redo before going further!" |
| `stage('Install Dependencies')` | 📦 | Download libraries your app needs (`npm install`) | Buying ingredients before cooking |
| `stage('Docker Build & Push')` | 🐳 | Build Docker image → push to registry (DockerHub/ECR) using saved login | Cook the food and deliver to restaurant (DockerHub) |
| `stage('Terraform')` | 🌍 | Run `terraform init → plan → apply` with AWS credentials to create/update infra | Using magic keys to auto-build the kitchen |
| `stage('Deploy to Kubernetes')` | ☸️ | Login to EKS cluster → update deployment with new image | Tell delivery truck: "Put fresh food on all tables (pods)" |
| `post { always / success / failure }` | 🔔 | Print nice message + emoji at the end (green check or red alert) | Teacher writes: "Great job!" or "See me after class" |

</details>

## 🔥 Why This Pipeline Rocks

- **Zero secrets in git** — all credentials live in Jenkins Credentials store
- **Quality first** — SonarQube gate stops bad code from going further
- **Reproducible builds** — unique image tags with build number
- **Infrastructure as Code** — Terraform handles cloud resources
- **GitOps-friendly** — easy to extend with ArgoCD later
- **One file does it all** — perfect for small/medium projects

## 🚀 Quick Start Checklist

1. Install required **Jenkins plugins**:
   - Pipeline
   - Docker Pipeline
   - SonarQube Scanner
   - Credentials Binding
   - AWS Credentials
   - NodeJS (or Maven)

2. Configure **Global Tools** in Jenkins:
   - NodeJS → name it `node20`
   - SonarQube Scanner → name it `sonar-scanner`

3. Add **Credentials** (Manage Jenkins → Credentials):
   - `git-creds` → GitHub username/password or PAT
   - `docker-creds` → Docker Hub / ECR login
   - `aws-creds` → AWS Access Key + Secret Key (for Terraform + EKS)
   - Sonar token → usually auto-linked via SonarQube server config

4. Configure **SonarQube** server in Jenkins (Manage Jenkins → System):
   - Name: `sonar-server`
   - URL: `http://your-sonarqube:9000`

5. Your repo should have:
   - `Dockerfile` (root)
   - `terraform/` folder with `.tf` files
   - Kubernetes manifests (or rely on `kubectl set image`)

6. Create Pipeline job → use this `Jenkinsfile`

Replace placeholders (`yourusername`, repo URL, cluster name, etc.) — and you're live! 🎉

Happy automating!  
Made with ❤️ for real-world DevOps projects

Last updated: March 2026
