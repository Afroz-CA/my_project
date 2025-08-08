
# **Afroz & Co. CA Consultation Website**

## **Project Overview**

**Afroz & Co. CA Consultation** is a static web application that offers a comprehensive online platform for businesses and individuals in Hyderabad to explore professional chartered accountancy services. The site provides a streamlined interface for browsing services such as accounting, taxation, auditing, business advisory, GST compliance, and financial planning. The goal is to simplify access to trusted financial solutions, helping clients achieve long-term financial growth and compliance.

This project demonstrates the deployment of **Afroz & Co.** using Azure App Services with deployment slots for seamless updates and zero-downtime deployments.

## **Problem Statement**

Many businesses and individuals face challenges in finding reliable and professional chartered accountancy services tailored to their needs. With complex financial regulations and diverse options, it can be overwhelming to make informed decisions about accounting, taxation, and advisory services. The challenge was to deploy a user-friendly website on Azure using a robust deployment strategy for efficient updates and high availability.

## **Project Goals**

- Deploy the **Afroz & Co.** website on Azure using App Services.
- Set up **deployment slots** for staging and production to ensure seamless updates.
- Host the static website and make it accessible via a custom domain: [https://afroz-ca.github.io/ca_site/](https://afroz-ca.github.io/ca_site/).
- Provide an intuitive interface for users to explore services and contact information.

## **Technologies and Azure Services Used**

1. **Azure CLI**: Used to create the resource group and manage Azure resources.
2. **Azure App Services**: Hosted the static website with scalability features.
3. **Azure Deployment Slots**: Enabled staging and production environments for updates.
4. **GitHub**: Hosted the website’s source code in a public repository.
5. **HTML/CSS/JavaScript**: Built the static frontend for a responsive experience.
6. **Git**: Used for version control and cloning the website onto Azure.

## **Project Steps**

### **1. Website Development**

- **Afroz & Co. Website**: A static web application developed using HTML, CSS, and JavaScript, offering a platform to explore accounting, taxation, auditing, business advisory, GST compliance, and financial planning services. Designed with user experience in mind, the site provides a streamlined interface for browsing services and contacting CA Afroz Begum.

**Screenshot**: [Path to Website Development Screenshot]

### **2. Deploying the Website on GitHub**

- The frontend of **Afroz & Co.** was uploaded to a public GitHub repository: [https://github.com/afroz-ca/ca_site](https://github.com/afroz-ca/ca_site).

**Screenshot**: [Path to GitHub Repository Setup Screenshot]

### **3. Azure Deployment Using App Services**

- **Resource Group**: Created using Azure CLI to hold all the resources.
  - Command:
    ```bash
    az group create --name AfrozCA_RG --location eastus
    ```

**Screenshot**: [Path to Resource Group Creation Screenshot]

- **App Service Plan**: Created to define the pricing and scaling tier.
  - Command:
    ```bash
    az appservice plan create --name AfrozCA_AppServicePlan --resource-group AfrozCA_RG --sku F1 --location eastus
    ```

**Screenshot**: [Path to App Service Plan Creation Screenshot]

- **Web App**: Created in Azure App Services to host the static website.
  - Command:
    ```bash
    az webapp create --resource-group AfrozCA_RG --plan AfrozCA_AppServicePlan --name AfrozCA-WebApp --runtime "NODE|18-lts"
    ```

**Screenshot**: [Path to Web App Creation Screenshot]

- **Deployment Source**: Configured continuous deployment from the GitHub repository.
  - Command:
    ```bash
    az webapp deployment source config --name AfrozCA-WebApp --resource-group AfrozCA_RG --repo-url https://github.com/afroz-ca/ca_site --branch main --manual-integration
    ```

**Screenshot**: [Path to Deployment Source Configuration Screenshot]

### **4. Deployment Slots Setup**

- **Staging Slot**: Created in Azure App Services for testing updates.
  - Command:
    ```bash
    az webapp deployment slot create --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging --configuration-source AfrozCA-WebApp
    ```

**Screenshot**: [Path to Staging Slot Creation Screenshot]

- **Deploy to Staging**: Pushed updates to the GitHub repository to trigger deployment to the staging slot.
  - Monitored deployment logs:
    ```bash
    az webapp log tail --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging
    ```

**Screenshot**: [Path to Staging Slot Deployment Screenshot]

- **Slot Swapping**: Configured to swap staging and production slots for zero-downtime updates.
  - Command:
    ```bash
    az webapp deployment slot swap --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging
    ```

**Screenshot**: [Path to Slot Swap Screenshot]

### **5. Custom Domain Configuration**

- Configured a custom domain for the web app.
  - Command:
    ```bash
    az webapp config hostname add --resource-group AfrozCA_RG --webapp-name AfrozCA-WebApp --hostname afroz-ca.github.io
    ```
- Verified domain ownership and configured SSL bindings for HTTPS.

**Screenshot**: [Path to Custom Domain Configuration Screenshot]

### **6. Testing and Accessing the Website**

- After deployment, the website was tested in the staging slot to verify functionality.
- Post-swapping, the website became accessible via the production slot at [https://afroz-ca.github.io/ca_site/](https://afroz-ca.github.io/ca_site/). Users can interact with **Afroz & Co.** to explore services and contact details.

**Screenshot**: [Path to Website Testing Screenshot]

## **Azure Services and Tools Used**

- **Azure CLI**: Resource group creation and management.
- **Azure App Services**: Hosting the static website.
- **Azure Deployment Slots**: Zero-downtime deployment management.
- **GitHub**: Version control and continuous deployment.
- **HTML/CSS/JavaScript**: Building the static website.
- **Git**: Managing the website’s codebase.

## **Live Website and Resources**

- **Website Link**: [https://afroz-ca.github.io/ca_site/](https://afroz-ca.github.io/ca_site/)
- **GitHub Repository**: [https://github.com/afroz-ca/ca_site](https://github.com/afroz-ca/ca_site)

**Screenshots**:

- **Created Resource Group Screenshot**  
  - [Path to Resource Group Creation Screenshot]

- **App Service Plan Creation Screenshot**  
  - [Path to App Service Plan Creation Screenshot]

- **Web App Creation Screenshot**  
  - [Path to Web App Creation Screenshot]

- **Deployment Source Configuration Screenshot**  
  - [Path to Deployment Source Configuration Screenshot]

- **Staging Slot Creation Screenshot**  
  - [Path to Staging Slot Creation Screenshot]

- **Staging Slot Deployment Screenshot**  
  - [Path to Staging Slot Deployment Screenshot]

- **Slot Swap Screenshot**  
  - [Path to Slot Swap Screenshot]

- **Custom Domain Configuration Screenshot**  
  - [Path to Custom Domain Configuration Screenshot]

- **Website Home Page Screenshot**  
  - [Path to Website Home Page Screenshot]

- **About Page Screenshot**  
  - [Path to About Page Screenshot]

- **Services Page Screenshot**  
  - [Path to Services Page Screenshot]

- **Contact Us Page Screenshot**  
  - [Path to Contact Us Page Screenshot]

## **Conclusion**

This project showcases the end-to-end process of deploying a static website using Azure App Services and deployment slots. By distributing updates through staging and production slots, we ensure high availability and seamless updates for the **Afroz & Co.** platform. The integration of Azure’s powerful tools and GitHub simplified the deployment and configuration process.
```
