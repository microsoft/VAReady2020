# Attaching a custom Skill
## Deploy a custom Skill
33. Create new project from Skill Template in Visual Studio. Give it a unique name and create it in the same directory your Virtual Assistant is in (i.e. if your Virtual Assistant is in `C:\Users\<USERNAME>\Source\Repos`, place the custom Skill there as well)
1. Build the solution to restore all packages
1. In a PowerShell Core window, navigate to the Skill's project directory, and run the following:
    ```
    ./Deployment/Scripts/deploy.ps1
    ```
1. You'll be prompted to enter the following:
    1. **Bot Name** - choose a unique name for the custom Skill. This will be used to create the AAD app registration and the resources
    1. **Azure resource group region**: eastus
    1. **Password for MSA app registration**: 16+ characters, 1+ special character(s), 1+ number(s)
    1. **Create a new LUIS Authoring Resource?**: y
    1. **LUIS Authoring Region**: westus

    Once you've entered the parameters, the script provisions the Skill's Azure resources. It also publishes the initial cognitive models to LUIS and publishes the bot project to the App Service
1. After successful completion, go to the Azure portal, and navigate to the Skill's `Web App Bot` resource
1. Note the name of the resource
1. Click the `Test in Webchat` blade to test your deployed Skill with the utterance _"sample dialog"_

## Connect the custom Skill to your Virtual Assistant
40. In the Skill project in Visual Studio, navigate to the `wwwroot\manifest` folder and open the `manifest-1.1`:

    1. Update `{YOUR_SKILL_URL}` with the URL of your deployed Skill endpoint (SKILL_AZURE_NAME.azurewebsites.net)

    1. Update `{YOUR_SKILL_APPID}` with the Active Directory AppID of your deployed Skill, you can find this within your `appSettings.json` file.
    1. Right-click on the project in the Solution Explorer window and select **Publish**
    1. Enter the details for the Skill's Web App in Azure, and click **Publish**
    1. Validate that you can retrieve the manifest from your Skill endpoint using the browser (`/manifest/manifest-1.1.json`)
36. Navigate to your Virtual Assistant project directory, and run the following:
    ```
    botskills connect --remoteManifest "http://<SKILL_AZURE_NAME>.azurewebsites.net/manifest/manifest-1.1.json" --luisFolder "..\..\<SKILL_PROJECT_NAME>\<SKILL_PROJECT_NAME>\Deployment\Resources\LU" --languages "en-us" --cs
    ```
    Once that command has run, your Skill is now connected to your local Virtual Assistant
1. Run your local Virtual Assistant
1. Open the Virtual Assistant configuration in the Emulator again. You should see the same welcome as before
1. Test the _"sample dialog"_ utterance in the Virtual Assistant to see that the Skill is connected
