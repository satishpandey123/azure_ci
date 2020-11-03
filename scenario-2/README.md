Macro Life, a healthcare company has recently setup the entire Network and Infrastructure on Azure.
The infrastructure has different components such as Virtual N/W, Subnets, NIC, IPs, NSG etc.
The IT team currently has developed PowerShell scripts to deploy each component where all the
properties of each resource is set using PowerShell commands.
The business has realized that the PowerShell scripts are growing over period of time and difficult to
handover when new admin onboards in the IT.
The IT team has now decided to move to ARM based deployment of all resources to Azure.
All the passwords are stored in a Azure Service known as key Vault. The deployments needs to be
automated using Azure DevOps using IaC(Infrastructure as Code).
1) What are different artifacts you need to create - name of the artifacts and its purpose
List of service which will be created to migrate on-premises infratructure to Azure:
    1. Virtual network defining CIDR bloack needed for the company.
	2. subnet for creat sub-network group for public and private resources.
	3. Route table - for defining access between different subnet and internet(in case of public subnet)
	4. VM in each subnet as per rquiremnet.
	5. Network interface for VMs
	6. Security groups for each VMS
	7. Blob storage for storing data in Azure
	8. Bastion host for accessing different resource of private network
	9. Nat gateway for private subnet to update patched from internet
	10. some more as the discussion goes on detailing.
	
2) List the tools you will to create and store the ARM templates.
Just needed a repo in which I can ceate arm template and add a link to directly create infrastructre on the fly. example as below
https://github.com/satishpandey123/quickstart-sas-viya-azure/tree/master/sas-viya

3) Explain the process and steps to create automated deployment pipeline.
 Integate it with jenkins of Azure devops pipeline to initiate the job.
4) Create a sample ARM template you will use to deploy a Windows VM of any size
Attached in the repo
5) Explain how will you access the password stored in Key Vault and use it as Admin Password in the VM
ARM template.

Creates a key vault with the enabledForTemplateDeployment property enabled. This property must be true before the template deployment process can access the secrets that are defined in the key vault.
Adds a secret to the key vault. The secret stores the VM administrator password.


"adminPassword": {
    "reference": {
        "keyVault": {
        "id": "/subscriptions/<SubscriptionID>/resourceGroups/mykeyvaultdeploymentrg/providers/Microsoft.KeyVault/vaults/<KeyVaultName>"
        },
        "secretName": "vmAdminPassword"
    }
},


