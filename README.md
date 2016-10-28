# Create a Storage Spaces Direct (S2D) Scale-Out File Server (SOFS) Cluster with Windows Server 2016 on an existing VNET
This template will create a Storage Spaces Direct (S2D) Scale-Out File Server (SOFS) cluster using Windows Server 2016 in an existing VNET and Active Directory environment.

This template creates the following resources:

+	A Premium Storage Account for storing VM disks for each storage node
+   A Standard Storage Account for a Cloud Witness
+	A Windows Server 2016 cluster for storage nodes, provisioned for Storage Spaces Direct (S2D) and the Scale-Out File Server (SOFS) role
+	One Availability Set for the cluster nodes, configured with five Update Domains and three Fault Domains

To deploy the required Azure VNET and Active Directory infrastructure, if not already in place, you may use the *DeployADOnly.json* template that is also located in this project. 

## Notes

+	The default settings for storage are to deploy using **premium storage**.  

+ 	The default settings for compute require that you have at least 2 cores of free quota to deploy.

+ 	The images used to create this deployment are
	+ 	Windows Server 2016 - Latest Image

+	To successfully deploy this template, be sure that the subnet to which the storage nodes are being deployed already exists on the specified Azure virtual network, AND this subnet should be defined in Active Directory Sites and Services for the appropriate AD site in which the closest domain controllers are configured.

+ To deploy the required Azure VNET and Active Directory infrastructure, if not already in place, you may use the *DeployADOnly.json* template that is also located in this project.

+ SPECIAL THANKS to <a href="https://github.com/mmarch">@mmarch</a> on code contributions for variable disk selection nested templates!

Click the button below to deploy from the portal

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Frobotechredmond%2F101-storage-spaces-direct%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Frobotechredmond%2F101-storage-spaces-direct%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

## Deploying Sample Templates

You can deploy these samples directly through the Azure Portal or by using the scripts supplied in the root of the repo.

To deploy a sammple using the Azure Portal, click the **Deploy to Azure** button found in the README.md of each sample.

To deploy the sample via the command line (using [Azure PowerShell or the Azure CLI](https://azure.microsoft.com/en-us/downloads/)) you can use the scripts.

Simple execute the script and pass in the folder name of the sample you want to deploy.  For example:

```PowerShell
.\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation 'eastus' -ArtifactsStagingDirectory '[foldername]'
```
```bash
azure-group-deploy.sh -a [foldername] -l eastus -u
```
If the sample has artifacts that need to be "staged" for deployment (Configuration Scripts, Nested Templates, DSC Packages) then set the upload switch on the command.
You can optionally specify a storage account to use, if so the storage account must already exist within the subscription.  If you don't want to specify a storage account
one will be created by the script or reused if it already exists (think of this as "temp" storage for AzureRM).

```PowerShell
.\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation 'eastus' -ArtifactsStagingDirectory '201-vm-custom-script-windows' -UploadArtifacts 
```
```bash
azure-group-deploy.sh -a '201-vm-custom-script-windows' -l eastus -u
```

Tags: ``cluster, ha, storage spaces, storage spaces direct, S2D``
