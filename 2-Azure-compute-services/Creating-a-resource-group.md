# Creating a resource group

Login using `az login`, and run:
```markdown
az group create --name <resource-grup-name> --location <my-location>
```
Example: `az group create --name resource-group-west --location westus2`

Note 1: To see list of all locations, you can run `az account list-locations -o table`

Note 2: A resource group can contain compute services from different regions

Note 3:
You can reference the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest&WT.mc_id=udacity_learn-wwl) for further information on other commands.