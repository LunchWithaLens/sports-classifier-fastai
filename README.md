"# sports-classifier-fastai" 
The code was based on the example at https://github.com/shankarj67/Water-classifier-fastai and some of my changes were due to fastai 24 -> 32, other maybe for Azure.

##Azure Deployment

My deployment steps were based on this Microsoft article https://docs.microsoft.com/en-us/azure/app-service/containers/quickstart-python

The initial steps executed in the Bash shell available in the Azure Portal (Cloud Shell)

  az account set --subscription "<your subscription name>"

  az webapp deployment user set --user-name <name> --password <password>

  az group create --name myPyWebGroup --location "West US 2"

I found that Basic and Stanard small AppService plans B1 and S1 failed to deploy - and in the logs I could see a 'Killed' during the pip install 

  az appservice plan create --name myPyWebAppServicePlan --resource-group myPyWebGroup --sku P1V2 --is-linux

  az webapp create --resource-group myPyWebGroup --plan myPyWebAppServicePlan --name sportsidentifier --runtime "PYTHON|3.6" --deployment-local-git
  
Once I had the Url returned from the previous command for the Git endpoint I could execute from my Git shell

  git remote add azure <url for Git endpoint from above command>

  git push azure master
  
In the Azure Portal for the Web App I could review the application logs to track down any issues.
