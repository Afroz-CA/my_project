Afroz & Co. CA Consultation Website
Project Overview
Afroz & Co. CA Consultation is a static web application designed to provide professional chartered accountancy services to businesses and individuals in Hyderabad. The website offers a user-friendly platform to explore services such as accounting, taxation, auditing, business advisory, GST compliance, and financial planning. Led by CA Afroz Begum, the site emphasizes personalized, reliable, and strategic financial solutions to support clients in achieving long-term financial growth.
This project demonstrates the deployment of the Afroz & Co. website using Azure App Services with deployment slots for seamless updates and zero-downtime deployments.
Problem Statement
Businesses and individuals in Hyderabad often struggle to find trusted, accessible, and professional chartered accountancy services tailored to their needs. The challenge was to create an intuitive online platform to showcase Afroz & Co.'s expertise and deploy it efficiently on Azure with a robust deployment strategy to ensure continuous availability and smooth updates.
Project Goals

Deploy the Afroz & Co. website on Azure App Services.
Implement deployment slots for staging and production to enable seamless updates and zero-downtime deployments.
Host the static website and make it accessible via a custom domain: https://afroz-ca.github.io/ca_site/.
Provide a streamlined interface for users to explore services, client success stories, and contact information.

Technologies and Azure Services Used

Azure CLI: Used to create and manage Azure resources.
Azure App Services: Hosted the static website with scalability and management features.
Azure Deployment Slots: Enabled staging and production environments for seamless updates.
GitHub: Hosted the website’s source code in a public repository.
HTML/CSS/JavaScript: Built the static frontend for a responsive and user-friendly experience.
Git: Used for version control and managing the website’s codebase.

Project Steps
1. Website Development

Afroz & Co. Website: Developed a static web application using HTML, CSS, and JavaScript. The site includes sections for About, Services, Client Success Stories, and Contact Us, designed with a focus on user experience and accessibility.
Ensured the website is responsive and optimized for various devices.

Screenshot: [Path to Website Development Screenshot]
2. Deploying the Website on GitHub

The frontend of Afroz & Co. was uploaded to a public GitHub repository: https://github.com/afroz-ca/ca_site.
Configured GitHub Pages as a backup hosting option.

Screenshot: [Path to GitHub Repository Setup Screenshot]
3. Azure Deployment Using App Services

Resource Group: Created using Azure CLI to hold all resources.
Command:az group create --name AfrozCA_RG --location eastus





Screenshot: [Path to Resource Group Creation Screenshot]

App Service Plan: Created to define the pricing and scaling tier for the web app.
Command:az appservice plan create --name AfrozCA_AppServicePlan --resource-group AfrozCA_RG --sku F1 --location eastus





Screenshot: [Path to App Service Plan Creation Screenshot]

Web App: Created in Azure App Services to host the static website.
Command:az webapp create --resource-group AfrozCA_RG --plan AfrozCA_AppServicePlan --name AfrozCA-WebApp --runtime "NODE|18-lts"





Screenshot: [Path to Web App Creation Screenshot]

Deployment Source: Configured continuous deployment from the GitHub repository.
Command:az webapp deployment source config --name AfrozCA-WebApp --resource-group AfrozCA_RG --repo-url https://github.com/afroz-ca/ca_site --branch main --manual-integration





Screenshot: [Path to Deployment Source Configuration Screenshot]
4. Deployment Slots Setup

Staging Slot: Created a staging slot for testing updates.
Command:az webapp deployment slot create --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging --configuration-source AfrozCA-WebApp





Screenshot: [Path to Staging Slot Creation Screenshot]

Deploy to Staging: Pushed updates to the GitHub repository to trigger deployment to the staging slot.
Monitored deployment logs:az webapp log tail --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging





Screenshot: [Path to Staging Slot Deployment Screenshot]

Slot Swapping: Swapped the staging slot with the production slot for zero-downtime updates.
Command:az webapp deployment slot swap --name AfrozCA-WebApp --resource-group AfrozCA_RG --slot staging





Screenshot: [Path to Slot Swap Screenshot]
5. Custom Domain Configuration

Configured a custom domain (afroz-ca.github.io) for the web app.
Command:az webapp config hostname add --resource-group AfrozCA_RG --webapp-name AfrozCA-WebApp --hostname afroz-ca.github.io




Verified domain ownership and configured SSL bindings for HTTPS.

Screenshot: [Path to Custom Domain Configuration Screenshot]
6. Testing and Accessing the Website

Tested the website in the staging slot to verify functionality, responsiveness, and content accuracy.
After swapping, validated the production slot to ensure the website is accessible via https://afroz-ca.github.io/ca_site/.
Ensured all sections (About, Services, Client Success Stories, Contact Us) render correctly across devices.

Screenshot: [Path to Website Testing Screenshot]
Azure Services and Tools Used

Azure CLI: Resource group creation and management.
Azure App Services: Hosting the static website.
Azure Deployment Slots: Enabling zero-downtime deployments.
GitHub: Version control and continuous deployment.
HTML/CSS/JavaScript: Building the static website.
Git: Managing the website’s codebase.

Live Website and Resources

Website Link: https://afroz-ca.github.io/ca_site/
GitHub Repository: https://github.com/afroz-ca/ca_site

Screenshots:

Created Resource Group Screenshot  

[Path to Resource Group Creation Screenshot]


App Service Plan Creation Screenshot  

[Path to App Service Plan Creation Screenshot]


Web App Creation Screenshot  

[Path to Web App Creation Screenshot]


Deployment Source Configuration Screenshot  

[Path to Deployment Source Configuration Screenshot]


Staging Slot Creation Screenshot  

[Path to Staging Slot Creation Screenshot]


Staging Slot Deployment Screenshot  

[Path to Staging Slot Deployment Screenshot]


Slot Swap Screenshot  

[Path to Slot Swap Screenshot]


Custom Domain Configuration Screenshot  

[Path to Custom Domain Configuration Screenshot]


Website Home Page Screenshot  

[Path to Website Home Page Screenshot]


About Page Screenshot  

[Path to About Page Screenshot]


Services Page Screenshot  

[Path to Services Page Screenshot]


Contact Us Page Screenshot  

[Path to Contact Us Page Screenshot]



Conclusion
This project showcases the end-to-end process of deploying the Afroz & Co. CA Consultation website using Azure App Services with deployment slots. By leveraging Azure’s infrastructure and GitHub for version control, the project ensures a scalable, reliable, and seamless deployment process. The use of deployment slots allows for continuous updates without interrupting user access, providing a professional and accessible platform for chartered accountancy services in Hyderabad.
