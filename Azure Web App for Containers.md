# Azure App Service Platform 
- Used to host Websites / backend
- Configure custom domains & SSL certificates
- Scale up or scale out
- Staging slots
- Easy to manage environment variables
- Rich monitoring experience
- Automated deployment
- IP Whitelisting, AD authentication
- Enabling a CDN

## Usage
- Create an App Service Plan
- No need to containerize 
- Also supports container hosting

## Why use web app for containers
- Consistent deployment model
- Supports more frameworks
- Control over framework versions
- Multi-container support (Docker-Compose or Kubernetes YAML)
- Sandboxed environment (Strong isolation)
- Trigger deployment from a container registry

## How to Deploy
- Create App service plan, Azure MySQL database, Azure Web App
- Deploy a wordpress container from Docker Hub

### Steps
- Create resource group
- Create app service Plan
- Create mysql server with mysqlServerName, adminUser and adminPassword 
- Open a firewall between app service and mysql server
  (az mysql server firewall-rule create -g $resourceGroup `
  --server $mysqlServerName --name AllowAppService `
  --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0)
  
- Set up an App Name
- Set up a dockerRepo name 

- Set up environment variables (web app config settings)

## Scaling out an App service plan 
- Set up number of workers
- Only can be done on "Stateless applications"

## Configuring continuous delivery
