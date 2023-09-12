# Terraform_code_of_private_AKS_cluster_for_adding_application_gateway
Using this techhub template we can create Azure private kubernetes cluster with application gateway using terraform module.
## Prerequisites

Before you can use this Terraform module, you will need to have the following installed:

- [Terraform](https://www.terraform.io/downloads.html) - v1.0.5 or later
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) - v2.26.0 or later

You will also need to have an Azure subscription and an existing resource group to deploy resources to. 

## Usage

To use this Terraform module, follow these steps:

Clone this Git repo to your local machine.

```bash
git clone git@github.com:NashTech-Labs/Terraform_code_of_private_AKS_cluster_for_adding_application_gateway.git
```

Change into the directory containing the module.

Initialize Terraform in the directory.

```bash
terraform init
```

Create a new file named `terraform.tfvars` in the same directory as your `.tf` files.

```bash
touch terraform.tfvars
```

Open the file in your preferred text editor.

```bash
nano terraform.tfvars
```

Add your desired inputs to the file in the following format:

```ruby
resource_group_name             = ""
location                        = ""
cluster_name                    = ""
kubernetes_version              = ""
system_node_count               = ""
vm_size                         = ""
node_pool_name                  = ""
enable_auto_scaling             = ""
aks_node_pool_type              = ""
os_disk_size_gb                 = ""
network_plugin                  = ""
network_policy                  = ""
loadbalancer_sku                = ""
identity_type                   = ""
workspace                       = ""
container_insights              = ""
aks_publisher                   = ""
aks_product                     = ""
private_cluster_public_fqdn_enabled = ""
aks_subnet_name                 = ""
aks_vnet_name                   = ""
aks_vnet_resource_group_name    = ""
application_gateway_name        = ""
application_gateway_subnet_name = ""
```

> Note that the `terraform.tfvars` file will not be committed to version control, as it could contain sensitive information such as access keys and credentials.

Review the changes that Terraform will make to your Azure resources.

```bash
terraform plan -var-file="terraform.tfvars"
```

Apply the changes to your Azure resources.

```bash
terraform apply -var-file="terraform.tfvars"
```

## Inputs

The module accepts the following inputs:

| Variable Name                       | Description                                                        | Type          | Default Value       |
|-------------------------------------|--------------------------------------------------------------------|---------------|---------------------|
| azure_client_id                     | Azure client ID                                                   |               |                     |
| azure_client_secret                 | Azure client secret                                               |               |                     |
| azure_tenant_id                     | Azure tenant ID                                                   |               |                     |
| azure_subscription_id               | Azure subscription ID                                             |               |                     |
| resource_group_name                 | RG name in Azure                                                  | string        | rg12                |
| location                            | Resources location in Azure                                       | string        | WestUS              |
| cluster_name                        | AKS name in Azure                                                 | string        | rg-aks              |
| kubernetes_version                  | Kubernetes version                                                | string        | 1.25.5              |
| system_node_count                   | Number of AKS worker nodes                                        | number        | 1                   |
| vm_size                             | Size of node pool                                                 | string        | Standard_DS2_v2     |
| node_pool_name                      | Node pool name                                                    | string        | vm               |
| enable_auto_scaling                 | Auto scaling node pool                                            | string        | false               |
| aks_node_pool_type                  | AKS node pool type                                                | string        | VirtualMachineScaleSets |
| os_disk_size_gb                     | Disk size in GB                                                   | number        | 30                  |
| network_plugin                      | Network plugin                                                    | string        | azure               |
| network_policy                      | Azure network policy                                              | string        | azure               |
| loadbalancer_sku                    | Specified load balancer SKU type                                  | string        | standard            |
| identity_type                       | Identity type                                                     | string        | SystemAssigned      |
| workspace                           | Log Analytics workspace name                                      | string        | aks-workspace       |
| container_insights                  | Name of the log analytics solution                               | string        | AksContainerInsights |
| aks_publisher                       | The publisher of the solution                                     | string        | Microsoft           |
| aks_product                         | The product name of the solution                                  | string        | aksContainerInsights |
| aks_subnet_name                     | Name of AKS Subnet                                                | string        |                     |
| aks_vnet_name                       | Name of AKS VNet                                                  | string        |                     |
| aks_vnet_resource_group_name        | Name of the AKS VNet resource group                               | string        |                     |
| private_cluster_public_fqdn_enabled | Disable a public FQDN on a new AKS cluster                        | bool          | false               |
| application_gateway_name            | Name of the application gateway to be attached with AKS           | string        |                     |
| application_gateway_subnet_name     | Name of the subnet where application gateway resides             | string        |                     |


You can modify this input by editing the `terraform.tfvars` file as described in the [Usage](#usage) section.

## Outputs

### AKS ID

The `aks_id` output represents the id of the AKS cluster and can be referenced in your Terraform code using `module.aks.aks_id`. 

### http application routing enabled
 
The HTTP application routing add-on makes it easy to access applications that are deployed to your Azure Kubernetes Service (AKS) cluster by:

    *Configuring an ingress controller in your AKS cluster.
    *Creating publicly accessible DNS names for application endpoints.
    *Creating a DNS zone in your subscription. For more information about DNS cost, see DNS pricing.
    
### identity type

Protect your applications and data at the front gate with Azure identity and access management solutions.

### network profile

Network profile is a network configuration template for Azure resources. It specifies certain network properties for the resource.

### azurerm log analytics workspace

Log Analytics workspace with which the solution will be linked.

### azurerm log analytics solution

Specifies the name of the log analytics solution to be deployed .

### role based access control enabled

Role-based access control (Azure RBAC) is a system that provides fine-grained access management of Azure resources.
