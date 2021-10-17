THIS IS THE README FILE FOR DEPLOYING THE AZURE SERVICE FABRIC CLUSTER USING ARM TEMPLATE.

DISCLAIMER: Default settings are used for some parameters

1. This directory contains the ARM template ("template.json") and the parameters template ("parameters.json") for the deployment of the Azure Service Fabric Cluster.

2. Deployment Steps using CD pipeline in Azure DevOps project.
	2.1 All the values for the parameters in the "parameters.json" will be populated using the Azure DevOps CD pipeline.
	2.2 The values can be CD parameters or can be retrieved from a "Customer Onboarding document" which provides customer information.
	2.3 The sensitive values can be retrieved from the Azure Key Vault.

3. Tasks in the deployment CD pipeline.
	3.1 Task-1: "Azure Key Vault"
		- Read the values from the Keyvault.
		- Arguments: "Subscription Service Connection Name" and "Key Vault Name"

	3.2 Task-2: "Replace Tokens"
		- Replace the values from KV in the "parameters.json" file
		- Arguments: "path/to/file/parameters.json" from the repo.

	3.3 Task-3: "ARM template deployment"
		- Setup task for deploying the Aure Service Fabric cluster using the ARM template.
		- Arguments:
			a. Deployment Scope: "Resource Group"
			b. ARM Connection: "Subscription Service Connection Name"
			c. Subscription: "Subscription Name"
			d. Action: "Create or Update Resource Group"
			e. Resource group: "Resource group name"
			f. Location: "Resource Location" (should be the same as "#{clusterLocation}#")
			g. Template location: "path/to/file/template.json"
			h. Template parameters: "path/to/file/parameters.json"
			i. Override template parameters: "Override params from the CD pipeline parameter values."

4. The above mentioned steps will created the Azure Service Fabric cluster in the mentioned subscription and resource group.
