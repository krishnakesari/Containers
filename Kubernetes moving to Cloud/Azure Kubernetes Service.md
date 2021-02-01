# Installations needed
1. Azure CLI
2. Register namespaces
3. Create resource group

# Check if installed properly 
1. use command az -v 
2. Log into your azure with az login
3. Register namespace 
   - az aks create --resource-group=kube-demo --name=demo-cluster --node-vm-size=Standard_D1 --generate-ssh-keys
4. Create a resource group use az group create --name kube-demo --location east
   - In the above kube-demo is the resource group
    
5. Create a Container Registry 
   - az acr create
    --resource-group
     --location
     --name
     --sku (decides level of features needed for a registry)
     
    az acr create -g kube-demo -l useast2 -n mydemoregistry8910 --sku Basic

# Push your application to AKS
<registry-name>.azurecr.io/<namespace>/<image-name>:<tag>
Example:
1. docker build -t demoregistry.azure.io/examples/demo:1.0 .
   alternative use:
2. docker tag 8e3458790f demoregistry.azure.io/examples/demo:1.0 .

Above:
1. <registry-name> - name of your registry to push to Eg: mydemoregistry8910
2. <namespace> - optional to organize repository
3. <image-name>:<tag> - choose an image name and tag for version control 


Steps:
1. Log in to Azure Container Registry (az acr login --name mydemoregistry8910)
2. Build a docker image (docker build -t mydemoregistry8910.azurecr.io/demo:1.0 .)   
3. Check docker images (docker images)   
4. Check if app is running properly (docker run -p 5001:5000 8c89b921b0a1)
5. Log In to registry (az acr login --name mydemoregistry8910)   
6. push image to container registry
- (docker push mydemoregistry8910.azurecr.io/demo:1.0 )
7. Create a cluster
   (az aks create)
   --resource-group [name of the resource]
   --name [defines cluster name]
   --node-vm-size [what size of vm to use for nodes]
- Example: az aks create --resource-group=kube-demo --name=demo-cluster --node-vm-size=Standard_D1 --generate-ssh-keys

## Create and deployment and service
- First get AKS credentials (az aks get-credentials --resource-group=kube-demo --name=demo-cluster)
- Get nodes using (kubectl get nodes)
- If created get pods using (kubectl get pods)

1. Run App in Kubernetes
- kubectl create deployment demo-app --image=mydemoregistry8910.azurecr.io/demo:1.0
2. Run Load balancer service
- kubectl expose deployment demo-app --type=LoadBalancer --port 5000 --target-port 5000
3. Get services from kubectl 
- kubectl get service
    
## Safely deleting resources created
1. Delete load balancer
- kubectl delete service demo-app
2. Delete cluster
- az aks delete -g kube-demo -n demo-cluster
3. Delete images
- az acr repository delete -n mydemoregistry8910 --image demo:1.0
4. Remove an entire resource group
- az group delete -n kube-demo

### Extra 
#### Scale Pods and Nodes
- kubectl scale deployment demo-app --replicas=3
- az aks scale -g kube-demo -n demo-cluster -c 5