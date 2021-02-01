# Azure Container Instance
- The Quickest way deploy container
- "Serverless" - you don't need to provision infrastructure
- Great for Quick experiments
- Per second billing model (Pay only while running container)

## Use Cases
- Not for permanently running containers
- Ideal for continuous integration build agents
- Ideal for multiple parallel builds
- Short-lived experiments (MongoDB or to perform load test)
- Batch jobs
- Elastic scale for Kubernetes clusters (Virtual Kubelet)

## Features
- Easy to create and Manage 
- Networking (Public IP address, Domain name prefix, Expose ports)
- Runs Windows or Linux containers
- Restart policy
- Allows mounting volumes (Azure file share, Secrets or Git Repos)
- Container Groups (every use will create container groups similar to Kubernetes pod or sidecar containers)

## Create Container Groups
- az group create
- az container create
- az container logs
- az group delete

## Pulling a container from Azure Container Registry into Azure Container Instance
- Checking samplewebapp in Azure Container Registry (az acr repository list -n $acrName --output table)
- Finding loginServer info ($acrServer = az acr show -n $acrName ` --query loginServer --output tsv)
- Checking loginServer name ($acrServer)
- Finding ACR Password ($acrPassword = az acr credential show -n $acrName ` --query "passwords[0].value" -o tsv)

- Storage account needed for file share

- Create Container Group
  (az container create -g $resourceGroup `
  -n $containerGroupName`
  --image $acrServer/samplewebapp:v2`
  --cpu 1 --memory 1`
  --registry-username $acrName`
  --registry-password $acrPassword`
  --azure-file-volume-account-name $storageAccountName `
  --azure-file-volume-account-key $storageKey`
  --azure-file-volume-share-name $shareName`
  --azure-file-volume-mount-path "/home"`
  -e TestSetting=FromAzCli TestFileLocation=/home/message.txt `
  --dns-name-label "aciacr1" --ports 80)
  







