# MERN Gallery Sample App - CI/CD Pipeline Guide

This document describes how to test, trigger, and manage the **CI/CD pipeline** for the MERN Gallery Sample App using **GitHub Actions**, **Docker**, **Ansible**, and **AWS EC2 instances** via a Bastion Host.

---

## CI/CD Workflows

| Workflow                | Trigger Condition | Purpose              |
|-------------------------|-------------------|----------------------|
| **deploy-backend.yml**  | Push to `backend/**` or manual dispatch | Builds Docker image for backend, pushes to Docker Hub, deploys to backend EC2 instances via Ansible |
| **deploy-frontend.yml** | Push to `frontend/**` or manual dispatch | Builds Docker image for frontend, pushes to Docker Hub, deploys to frontend EC2 instances via Ansible |
| **main.yml**            | Push to `main` branch or manual dispatch | Deploys both backend and frontend together | NOTE: THIS IS CURRENTLY DISABLED |

---

## How to Trigger the Pipelines

### Automatically on Code Push
- Push code changes to:
  - `/backend/**` → triggers `deploy-backend.yml`
  - `/frontend/**` → triggers `deploy-frontend.yml`
  - `/main` branch → triggers `main.yml` (deploys both backend & frontend)

### Manually via GitHub Actions
1. Go to your GitHub repository.
2. Navigate to **Actions** tab.
3. Select the desired workflow (`Deploy Backend Only`, `Deploy Frontend Only`, or `Build and Deploy via Bastion`).
4. Click **Run workflow**.

---

## Verifying Deployment

1. **Check GitHub Actions Logs**
   - Navigate to **Actions** tab in GitHub.
   - Inspect logs for each step in the pipeline.

2. **Verify Docker Images on EC2-OPTIONAL**
   ```bash
   docker images
