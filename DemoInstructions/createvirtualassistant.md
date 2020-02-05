# Creating a base Virtual Assistant
10. Open Visual Studio 2019, and create a new project from the Virtual Assistant Template. Give it a unique name
1. Build the solution in VS19 to restore all NuGet packages
1. Open a PowerShell Core window, and set up your environment with the following. You'll be prompted to login
    ```
    az login
    ```
1. Then, you'll see all of your subscriptions. Choose the one you want to use, and run:
    ```
    az account set --subscription <SUBSCRIPTION_NAME_OR_ID>
    ````
1. Navigate to the project directory of your Virtual Assistant, and run the following command:
    ```
    ./Deployment/Scripts/deploy.ps1
    ```
1. You'll be prompted to enter the following:
    1. **Bot Name** - choose a unique name for the Virtual Assistant. This will be used to create the AAD app registration and the resources
    1. **Azure resource group region**: eastus
    1. **Password for MSA app registration**: 16+ characters, 1+ special character(s), 1+ number(s)
    1. **Create a new LUIS Authoring Resource?**: y
    1. **LUIS Authoring Region**: westus

1. Once you've entered the parameters, the script provisions the Virtual Assistant's Azure resources. It also publishes the initial cognitive models to LUIS/QnA Maker and publishes the bot project to the App Service
1. After successful completion, go to the Azure portal, and navigate to your Virtual Assistant's `Web App Bot` resource
1. Click the `Test in Webchat` blade to test your deployed Virtual Assistant
