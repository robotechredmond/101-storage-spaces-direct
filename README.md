# Create a Storage Spaces Direct (S2D) Cluster with Windows Server 2016 on an existing VNET
This template will create a Storage Spaces Direct (S2D) cluster using Windows Server 2016 in an existing VNET and Active Directory environment.

This template creates the following resources:

+	Three Premium Storage Accounts for storage nodes
+	Three VMs in a Windows Server 2016 cluster as storage nodes, provisioned for Storage Spaces Direct (S2D)
+	One Availability Set for the cluster nodes, configured with five Update Domains and three Fault Domains

To deploy the required Azure VNET and Active Directory infrastructure, if not already in place, you may use the *DeployADOnly.json* template that is also located in this project. 

## Notes

+	The default settings for storage are to deploy using **premium storage**.  

+ 	The default settings for compute require that you have at least 3 cores of free quota to deploy.

+ 	The images used to create this deployment are
	+ 	Windows Server 2016 - Latest Image

+	To successfully deploy this template, be sure that the subnet to which the storage nodes are being deployed already exists on the specified Azure virtual network, AND this subnet should be defined in Active Directory Sites and Services for the appropriate AD site in which the closest domain controllers are configured.

+ To deploy the required Azure VNET and Active Directory infrastructure, if not already in place, you may use the *DeployADOnly.json* template that is also located in this project.

Click the button below to deploy from the portal

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frobotechredmond%2F101-storage-spaces-direct%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Frobotechredmond%2F101-storage-spaces-direct%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

## Deploying from PowerShell

For details on how to install and configure Azure Powershell see [here].(https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)

Launch a PowerShell console

Change working folder to the folder containing this template

```PowerShell

New-AzureRmResourceGroup -Name "<new resourcegroup name>" -Location "<new resourcegroup location>"  -TemplateParameterFile .\azuredeploy-parameters.json -TemplateFile .\azuredeploy.json

```

Tags: ``cluster, ha, storage spaces, storage spaces direct, S2D``
