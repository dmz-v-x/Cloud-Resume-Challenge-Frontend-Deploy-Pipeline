# 🚀 Frontend Deployment Pipeline – Cloud Resume Challenge

This repository contains the **GitHub Actions workflow** to deploy the static frontend of the **Cloud Resume Challenge** to an AWS S3 bucket, along with automatic CloudFront cache invalidation.

---

## 📦 What this Repository Does

- Pulls the built frontend (`out/` folder) from a private GitHub repository.
- Uploads the latest frontend files to an S3 bucket hosting the website.
- Invalidates the CloudFront distribution cache to ensure users see the newest version immediately.
- Secures AWS access using **OIDC (OpenID Connect)** — no long-term AWS credentials are stored in GitHub.

---

## 📂 Repository Structure

| File/Folder | Purpose |
|:-----------:|:--------|
| `.github/workflows/deploy.yml` | GitHub Actions workflow that handles deployment |

---

## 🔧 Setup Instructions

### 1. Create Two Repositories
- **Private Repo**: Contains the built `out/` folder (static frontend files).
- **Public Repo**: Contains this GitHub Actions workflow to deploy to AWS.

### 2. AWS Setup
- Create an **IAM Role** with **OIDC Trust Policy** allowing GitHub to assume the role.
- Attach permissions for:
  - S3 upload
  - CloudFront invalidation (optional)

### 3. GitHub Secrets to Add

| Secret Key | Description |
|:----------:|:------------|
| `AWS_ROLE_ARN` | IAM Role ARN that GitHub Actions assumes |
| `AWS_REGION` | AWS region (e.g., `ap-south-1`) |
| `PRIVATE_REPO_PAT` | GitHub Personal Access Token to clone the private repo |
| `CLOUDFRONT_DISTRIBUTION_ID` | (Optional) CloudFront Distribution ID for cache invalidation |

### 4. Trigger Deployment
- Push a change to the **main branch**.
- Or manually trigger via **GitHub Actions ➔ Run workflow**.

---

## 🔐 Security Considerations

- **No AWS keys** stored in GitHub — OIDC dynamically issues short-lived credentials.
- **Private repository** used for storing frontend build output.
- **CloudFront invalidation** ensures users always see the latest version.

---

## 🏆 Part of the Cloud Resume Challenge

This deployment pipeline is part of the broader [Cloud Resume Challenge](https://cloudresumechallenge.dev/), demonstrating skills in:
- GitHub Actions
- AWS S3 / CloudFront
- IAM Roles & OIDC Authentication
- CI/CD Pipelines

---

