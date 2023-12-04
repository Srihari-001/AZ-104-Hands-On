# Add, Remove, and Update Tags for Resources in Azure

## Introduction
In this hands-on lab scenario, the finance department has requested additional taxonomy information on a recent Azure bill. They are interested in details such as who created the resources, which department budget should be used, and whether the resources are essential for running business-critical systems.

## Solution

1. **Log in to Azure Portal:**
   - Open Azure Portal and use the provided credentials.

2. **Access Cloud Shell:**
   - Click the Cloud Shell icon (>_ ) in the upper right.
   - Select bash.
   - Click Show advanced settings.
   - Use the same region as the lab provided storage account and the existing resource group. Create a new Storage account (use a globally unique name).
   - For File share, select Create new and name it "fileshare".
   - Click Create storage. (If issues, use the existing storage account).

3. **Add Tags to the Resource Group:**
   - List resource groups:
     ```bash
     az group list
     ```
   - Copy the group name.
   - Update the resource group tags:
     ```bash
     az group update --resource-group "<RESOURCE_GROUP_NAME>" --tags "Environment=Production" "Dept=IT" "CreatedBy=<YourName>"
     ```

4. **Remove Tags for VM and Mark for Deletion:**
   - List existing virtual machines:
     ```bash
     az vm list --query '[].{name:name, resourceGroup:resourceGroup, tags:tags}' -o json
     ```
   - Remove existing tags from the VM:
     ```bash
     az vm update -g "<RESOURCE_GROUP_NAME>" -n webvm1 --remove tags.defaultExperience
     ```
   - Mark the VM for deletion:
     ```bash
     az vm update -g "<RESOURCE_GROUP_NAME>" -n webvm1 --set tags.MarkForDeletion=Yes
     ```

5. **Change Tags for the Virtual Network:**
   - List virtual networks:
     ```bash
     az network vnet list --query '[].{name:name, resourceGroup:resourceGroup, tags:tags}' -o json
     ```
   - Overwrite existing tags for the virtual network:
     ```bash
     az resource tag --tags "Dept=IT" "Environment=Production" "CreatedBy=<YourName>" --resource-group "<RESOURCE_GROUP_NAME>" -n "vnet1" --resource-type "Microsoft.Network/virtualNetworks"
     ```

## Conclusion
Congratulations! You've completed this hands-on lab.
