
# Deploying a Static Website on Azure App Service with Deployment Slots

This project demonstrates deploying a static website using **Azure App Service** with **GitHub** integration and **deployment slots** for seamless updates via a CI/CD pipeline. This README explains Azure App Service, deployment slots, and provides a detailed guide to deploy the website and swap slots.

## Table of Contents
- [Azure App Service Overview](#azure-app-service-overview)
- [Deployment Slots Overview](#deployment-slots-overview)
- [Prerequisites](#prerequisites)
- [Deployment Steps](#deployment-steps)
  - [1. Create a Resource Group](#1-create-a-resource-group)
  - [2. Create an App Service Plan](#2-create-an-app-service-plan)
  - [3. Create a Web App](#3-create-a-web-app)
  - [4. Set Up a GitHub Repository](#4-set-up-a-github-repository)
  - [5. Push Website Code to GitHub](#5-push-website-code-to-github)
  - [6. Configure CI/CD with GitHub](#6-configure-cicd-with-github)
  - [7. Create a Staging Deployment Slot](#7-create-a-staging-deployment-slot)
  - [8. Deploy to Staging Slot](#8-deploy-to-staging-slot)
  - [9. Swap Staging with Production](#9-swap-staging-with-production)
  - [10. Verify Deployment](#10-verify-deployment)
- [Screenshots](#screenshots)
- [Conclusion](#conclusion)

## Azure App Service Overview
**Azure App Service** is a managed platform-as-a-service (PaaS) by Microsoft Azure for hosting web applications, including static websites (HTML, CSS, JavaScript). It handles infrastructure tasks like server management, scaling, and security, allowing developers to focus on code. It supports multiple languages and integrates with GitHub for automated deployments.

## Deployment Slots Overview
**Deployment Slots** are isolated environments within an Azure App Service instance, enabling you to deploy and test different versions of your app (e.g., staging, production). Each slot has a unique URL and settings, allowing you to validate changes in staging before swapping to production with zero downtime.

## Prerequisites
- **Azure Account**: Active subscription (free trial available at [azure.microsoft.com](https://azure.microsoft.com)).
- **GitHub Account**: For hosting your website code.
- **Git**: Installed locally for version control.
- **Static Website Files**: HTML, CSS, JavaScript files ready for deployment.
- **Azure CLI** (optional): For CLI-based management ([install guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)).
- **Code Editor**: E.g., Visual Studio Code.

## Deployment Steps


### 1. Create a Resource Group with Azure CLI
A resource group organizes Azure resources.

1. Open a terminal (e.g., Command Prompt, PowerShell, or Bash).
2. Log in to Azure CLI:
   ```bash
   az login
   ```
   Follow the browser prompt to authenticate.
3. Create a resource group:
   ```bash
   az group create --name my-static-web-rg --location eastus
   ```
   - Replace `eastus` with your preferred region (e.g., `westus`, `centralus`).
   **Screenshot**: Capture the terminal output of the `az group create` command and save as `screenshots/resource-group-creation.png`.
4. Verify the resource group exists:
   - Option 1: Check in the Azure Portal under **Resource Groups**.
   - Option 2: Run the following command:
     ```bash
     az group show --name my-static-web-rg
     ```
   **Screenshot (Optional)**: Capture the terminal output of `az group show` or the Azure Portal Resource Groups page and save as `screenshots/resource-group-verification.png`.

### 2. Create an App Service Plan
With the resource group `my-static-web-rg` created, define the compute resources for your web app.

1. In the Azure Portal, search for **App Service Plans**.
2. Click **+ Create**.
3. Configure:
   - **Subscription**: Your subscription.
   - **Resource Group**: `my-static-web-rg`.
   - **Name**: `my-static-app-plan`.
   - **OS**: Linux (recommended for static sites).
   - **Region**: `East US` (match resource group).
   - **Pricing Tier**: Free F1 or as needed.
4. Click **Review + Create**, then **Create**.

**Screenshot**: Save as `screenshots/app-service-plan.png`.

### 3. Create a Web App
Host your static website.

1. In Azure Portal, search for **App Services**.
2. Click **+ Create** > **Web App**.
3. Configure:
   - **Subscription**: Your subscription.
   - **Resource Group**: `my-static-web-rg`.
   - **Name**: `my-static-web-app` (must be unique).
   - **Publish**: Code.
   - **Runtime Stack**: PHP 8.1 (for static HTML on Linux).
   - **OS**: Linux.
   - **Region**: Same as above.
   - **App Service Plan**: `my-static-app-plan`.
4. Click **Review + Create**, then **Create**.
5. Note the **Default Domain** (e.g., `https://my-static-web-app.azurewebsites.net`).

**Screenshot**: Save as `screenshots/web-app-creation.png`.

### 4. Set Up a GitHub Repository
Host your code on GitHub.

1. Log in to [GitHub](https://github.com).
2. Click **+ New Repository**.
3. Configure:
   - **Name**: `static-website`.
   - **Visibility**: Public or Private.
   - **Initialize with README**: Optional.
4. Click **Create Repository**.

**Screenshot**: Save as `screenshots/github-repo-creation.png`.

### 5. Push Website Code to GitHub
Upload your static website files.

1. Open your project folder in a code editor.
2. Initialize Git and push code:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<your-username>/static-website.git
   git push -u origin main
   ```
3. Verify files in GitHub repository.

**Screenshot**: Save as `screenshots/github-repo-files.png`.

### 6. Configure CI/CD with GitHub
Automate deployment to Azure.

1. In Azure Portal, go to your web app’s **Deployment Center**.
2. Select **Source**: GitHub.
3. Authorize Azure to access GitHub.
4. Configure:
   - **Organization**: Your GitHub account.
   - **Repository**: `static-website`.
   - **Branch**: `main`.
5. Click **Save** to create a GitHub Actions workflow.
6. Check the **Actions** tab in GitHub for workflow status.
7. Verify the site at the **Default Domain** URL.

**Screenshot**: Save as `screenshots/deployment-center.png`.

### 7. Create a Staging Deployment Slot
Test updates in a separate environment.

1. In your web app, go to **Deployment Slots**.
2. Click **+ Add Slot**.
3. Enter:
   - **Name**: `staging`.
   - **Clone Settings**: Optional (clone from production).
4. Click **Add**.
5. Note the staging URL (e.g., `https://my-static-web-app-staging.azurewebsites.net`).

**Screenshot**: Save as `screenshots/staging-slot-creation.png`.

### 8. Deploy to Staging Slot
Deploy updates to the staging slot.

1. In GitHub, create a `staging` branch:
   ```bash
   git checkout -b staging
   git push origin staging
   ```
2. In Azure Portal, go to the **staging** slot’s **Deployment Center**.
3. Configure to use the `staging` branch (as in Step 6).
4. Update code locally, commit, and push:
   ```bash
   git add .
   git commit -m "Staging updates"
   git push origin staging
   ```
5. Verify changes at the staging URL.

**Screenshot**: Save as `screenshots/staging-deployment-center.png`.

### 9. Swap Staging with Production
Promote staging changes to production.

1. In **Deployment Slots**, select the **staging** slot.
2. Click **Swap**.
3. Configure:
   - **Source**: `staging`.
   - **Destination**: `Production`.
   - **Swap Type**: Swap.
4. Click **Swap**.

**Screenshot**: Save as `screenshots/slot-swap.png`.

### 10. Verify Deployment
Ensure production reflects staging changes.

1. Visit the production URL (e.g., `https://my-static-web-app.azurewebsites.net`).
2. Confirm updated content displays.
3. Check GitHub Actions logs for deployment status.

**Screenshot**: Save as `screenshots/production-website.png`.

## Screenshots
Upload the following to the `screenshots/` folder in your GitHub repository:
- `resource-group-creation.png`: Resource group creation.
- `app-service-plan.png`: App Service Plan creation.
- `web-app-creation.png`: Web app creation.
- `github-repo-creation.png`: GitHub repository creation.
- `github-repo-files.png`: Repository with uploaded files.
- `deployment-center.png`: Production slot Deployment Center.
- `staging-slot-creation.png`: Staging slot creation.
- `staging-deployment-center.png`: Staging slot Deployment Center.
- `slot-swap.png`: Slot swap configuration.
- `production-website.png`: Live production site.

## Conclusion
You’ve deployed a static website to Azure App Service with GitHub CI/CD and used deployment slots for zero-downtime updates. This setup enables efficient testing and deployment. Explore further Azure features like custom domains or scaling for advanced use cases.

**Resources**:
- [Azure App Service Docs](https://learn.microsoft.com/en-us/azure/app-service/)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
```

