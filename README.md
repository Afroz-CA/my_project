# my_project
Afroz & Co. CA Consultation Website
Project Overview
Afroz & Co. CA Consultation is a static web application designed to provide professional chartered accountancy services to businesses and individuals in Hyderabad. The website offers a user-friendly platform to explore services such as accounting, taxation, auditing, business advisory, GST compliance, and financial planning. Led by CA Afroz Begum, the site emphasizes personalized, reliable, and strategic financial solutions to support clients in achieving long-term financial growth.
This project demonstrates the deployment of the Afroz & Co. website using Azure App Services, with deployment slots for seamless updates and swapping to ensure zero-downtime deployments.
Problem Statement
Businesses and individuals in Hyderabad often struggle to find trusted, accessible, and professional chartered accountancy services tailored to their needs. The challenge was to create an intuitive online platform to showcase Afroz & Co.'s expertise and deploy it efficiently on Azure with a robust deployment strategy to ensure continuous availability and smooth updates.
Project Goals

Deploy the Afroz & Co. static website on Azure App Services.
Implement deployment slots for staging and production to enable seamless updates and zero-downtime deployments.
Ensure the website is accessible via a custom domain: https://afroz-ca.github.io/ca_site/.
Provide a streamlined interface for users to explore services, client success stories, and contact information.

Technologies and Azure Services Used

Azure App Services: Hosted the static website with scalability and management features.
Azure Deployment Slots: Enabled staging and production environments for seamless swapping and updates.
GitHub: Hosted the website's source code in a public repository.
HTML/CSS/JavaScript: Built the static frontend for a responsive and user-friendly experience.
Azure CLI: Used for managing Azure resources and deployments.
Git: Version control for managing the website's codebase.

Project Steps
1. Website Development

Afroz & Co. Website: Developed a static web application using HTML, CSS, and JavaScript. The site includes sections for About, Services, Client Success Stories, and Contact Us, designed with a focus on user experience and accessibility.
Ensured the website is responsive and optimized for various devices.

Screenshot: [Path to Website Development Screenshot]
2. Hosting the Website on GitHub

Created a public GitHub repository to host the website's source code.
Uploaded the frontend code (HTML, CSS, JavaScript files) to the repository: https://github.com/afroz-ca/ca_site.
Configured the repository for GitHub Pages to serve as a backup hosting option.

Screenshot: [Path to GitHub Repository Setup Screenshot]
3. Azure Deployment Using App Services
Step 3.1: Login to Azure Portal

Access the Azure Portal (https://portal.azure.com) using valid credentials.
Ensure an active Azure subscription is available.

Screenshot: [Path to Azure Portal Login Screenshot]
Step 3.2: Create a Resource Group

In the Azure Portal, navigate to Resource Groups and click Create.
Specify a resource group name (e.g., AfrozCA_RG) and select a region (e.g., East US).
Use Azure CLI command for automation:az group create --name AfrozCA_RG --location eastus


Verify the resource group creation in the portal.

Screenshot: [Path to Resource Group Creation Screenshot]
Step 3.3: Create an App Service Plan

Navigate to App Service Plans in the Azure Portal and click Create.
Select the resource group (AfrozCA_RG), provide a plan name (e.g., AfrozCA_AppServicePlan), and choose a pricing tier (e.g., F1 Free or B1 Basic for production).
Use Azure CLI:az appservice plan create --name AfrozCA_AppServicePlan --resource-group AfrozCA_RG --sku F1 --location eastus


Confirm the plan is created and visible in the portal.

Screenshot: [Path to App Service Plan Creation Screenshot]
Step 3.4: Create a Web App in Azure App Services

Navigate to App Services and click Create > Web App.
Configure the web app:
Resource Group: AfrozCA_RG
Name: A unique name (e.g., AfrozCA-WebApp)
Publish: Code
Runtime Stack: Node.js (for static sites, as Azure App Services uses Node.js to serve static content)
App Service Plan: AfrozCA_AppServicePlan
Region: East US


Use Azure CLI:az webapp create --resource-group AfrozCA_RG --plan AfrozCA_AppServicePlan --name AfrozCA-WebApp --runtime "NODE|18-lts"


Verify the web app is created and accessible via a default Azure URL (e.g., https://AfrozCA-WebApp.azurewebsites.net).

Screenshot: [Path to Web App Creation Screenshot]
Step 3.5: Configure Deployment Source

In the Azure Portal, navigate to the web app (AfrozCA-WebApp) and select Deployment Center.
Choose GitHub as the source control.
Authenticate with GitHub and select the repository (afroz-ca/ca_site) and branch (e.g., main).
Configure continuous deployment to automatically deploy changes pushed to the repository.
Use Azure CLI to link the repository:az webapp deployment source config --name AfrozCA-WebApp --resource-group AfrozCA_RG --repo-url https://github.com/afroz-ca/ca_site --branch main --manual-integration


Verify the deployment pipeline is set up and the initial deployment is successful.

Screenshot: [Path to Deployment Source Configuration Screenshot]
Step 3.6: Create a Staging Deployment Slot

In the Azure Portal, navigate to the web app (AfrozCA-WebApp) and select Deployment slots > Add Slot.
Name the slot (e.g., staging) and clone settings from the production slot.
Use Azure CLI:az webapp deployment slot create --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging --configuration-source AfrozCA-WebApp


Verify the staging slot is created and accessible via a URL (e.g., https://AfrozCA-WebApp-staging.azurewebsites.net).

Screenshot: [Path to Staging Slot Creation Screenshot]
Step 3.7: Deploy to Staging Slot

Push updates to the GitHub repository (afroz-ca/ca_site) to trigger deployment to the staging slot.
Test the website in the staging slot to ensure new features or updates work as expected.
Monitor the deployment logs in the Azure Portal under Deployment Center or use Azure CLI:az webapp log tail --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging



Screenshot: [Path to Staging Slot Deployment Screenshot]
Step 3.8: Swap Staging and Production Slots

Once the staging slot is verified, navigate to Deployment slots in the Azure Portal and select Swap.
Swap the staging slot with the production slot to deploy updates to the live site.
Use Azure CLI:az webapp deployment slot swap --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging


Verify the production slot now reflects the updates and is accessible via the production URL.

Screenshot: [Path to Slot Swap Screenshot]
Step 3.9: Configure Custom Domain

In the Azure Portal, navigate to the web app (AfrozCA-WebApp) and select Custom domains.
Add a custom domain (e.g., afroz-ca.github.io) by configuring DNS settings with the domain provider.
Verify domain ownership and configure SSL bindings for HTTPS.
Use Azure CLI to add the custom domain:az webapp config hostname add --resource-group AfrozCA_RG --webapp-name AfrozCA-WebApp --hostname afroz-ca.github.io


Verify the website is accessible via https://afroz-ca.github.io/ca_site/.

Screenshot: [Path to Custom Domain Configuration Screenshot]
4. Testing and Accessing the Website

Tested the website in the staging slot to verify functionality, responsiveness, and content accuracy.
After swapping, validated the production slot to ensure the website is fully functional and accessible via https://afroz-ca.github.io/ca_site/.
Ensured all sections (About, Services, Client Success Stories, Contact Us) are rendering correctly across devices.

Screenshot: [Path to Website Testing Screenshot]
Azure Services and Tools Used

Azure App Services: Hosting the static website with high availability and scalability.
Azure Deployment Slots: Enabling zero-downtime deployments through staging and production slots.
Azure CLI: Managing resource creation, deployment configurations, and slot management.
GitHub: Hosting the website's source code and enabling continuous deployment.
HTML/CSS/JavaScript: Building a responsive and user-friendly static website.

Live Website and Resources

Website Link: https://afroz-ca.github.io/ca_site/
GitHub Repository: https://github.com/afroz-ca/ca_site

Conclusion
This project demonstrates the end-to-end process of deploying the Afroz & Co. CA Consultation website using Azure App Services and deployment slots. By leveraging Azure's infrastructure and GitHub for version control, the project ensures a scalable, reliable, and seamless deployment process. The use of deployment slots allows for continuous updates without interrupting user access, providing a professional and accessible platform for chartered accountancy services in Hyderabad.
