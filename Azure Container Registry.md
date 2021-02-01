## Azure Container Registry
- Share images with other developers or Azure
- Store containers in Azure
- Can build images automatically

### Create ACR using
- Azure portal, Powershell, Azure CLI (cloud shell in Azure Portal)
- Restrict access rights
- added security layers

### Push Images 
1. Log in to ACR (az acr login -n $registryName)
2. Find log in server name ($loginServer = az acr show -n $registryName ` --query loginServer --output tsv)
3. See loginServer name using ($loginServer)
4. see all docker images (docker image ls)
5. tag docker image with loginServer (docker tag image:v2 loginServer/image:v2)
6. push image (push $loginServer/image:v2)
7. To check the pushed image (az acr repository list -n $registryName -o table)
