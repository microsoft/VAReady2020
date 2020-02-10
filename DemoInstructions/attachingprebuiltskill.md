# Attaching a pre-built Skill
aka.ms/VAReadyDemo2

## Deploy the pre-built Skill
18. Clone the [Bot Framework Solutions repo](https://github.com/microsoft/botframework-solutions)
1. Open the [pre-built Point Of Interest Skill](https://microsoft.github.io/botframework-solutions/skills/samples/point-of-interest/)  ([/skills/csharp/pointofinterestskill/](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp/pointofinterestskill)) project in Visual Studio. 
    
    NOTE: This project uses common files outside of its own directory, so for the purposes of this workshop, don't move the pointofinterestskill folder from the repo.
    
1. In a PowerShell Core window, navigate to the Skill's project directory, and run the following:
    ```
    ./Deployment/Scripts/deploy.ps1
    ```
1. You'll be prompted to enter the following:
    1. **Bot Name** - choose a unique name for the pre-built Skill. This will be used to create the AAD app registration and the resources
    1. **Azure resource group region**: eastus
    1. **Password for MSA app registration**: 16+ characters, 1+ special character(s), 1+ number(s)
    1. **Create a new LUIS Authoring Resource?**: y
    1. **LUIS Authoring Region**: westus
    
    Once you've entered the parameters, the script provisions the Skill's Azure resources. It also publishes the initial cognitive models to LUIS and publishes the bot project to the App Service
1. After successful completion, go to the Azure portal, and navigate to the skill's `Web App Bot` resource
1. Note the name of the resource
1. Click the `Test in Webchat` blade to test an utterance from the Point Of Interest Skill, such as _"Can you recommend a restaurant in Seattle?"_



## Connect the pre-built Skill to your Virtual Assistant
25. In the Skill project in Visual Studio, navigate to the `wwwroot\manifest` folder and open the `manifest-1.1`:

    1. Update `{YOUR_SKILL_URL}` with the URL of your deployed Skill endpoint (POI_SKILL_AZURE_NAME.azurewebsites.net)

    1. Update `{YOUR_SKILL_APPID}` with the Active Directory AppID of your deployed Skill, you can find this within your `appSettings.json` file.
    1. Right-click on the project in the Solution Explorer window and select **Publish**
    1. Enter the details for the Skill's Web App in Azure, and click **Publish**
    1. Validate that you can retrieve the manifest from your Skill endpoint using the browser (`/manifest/manifest-1.1.json`)
1. Navigate to your Virtual Assistant project directory, and run the following:
    ```
    botskills connect --remoteManifest "http://<POI_SKILL_AZURE_NAME>.azurewebsites.net/manifest/manifest-1.1.json" --luisFolder "<PATH_TO_POI_SKILL_PROJECT>\Deployment\Resources\LU" --languages "en-us" --cs
    ```
    Once that command has run, your Skill is now connected to your local Virtual Assistant
1. Run your local Virtual Assistant

1. Open the Emulator to test the local Virtual Assistant
1. Click `create a new bot configuration` and enter the following:
    1. **Bot name**: Virtual Assistant
    1. **Endpoint url**: http://localhost:3978/api/messages
    1. **Microsoft App ID**: Copy-paste the "microsoftAppId" from the Virtual Assistant's `appsettings.json`
    1. **Microsoft App password**: Copy-paste the "microsoftAppPassword" from the Virtual Assistant's `appsettings.json`
1. Click `Save and connect` to run your bot
1. Once the Emulator connects to the endpoint, you should see the same welcome as before
1. Test an utterance from the Point Of Interest Skill, such as _"Can you recommend a restaurant in Seattle?"_ to see that the Skill is connected to the Virtual Assistant


[**Next, attach a custom Skill.**](https://github.com/microsoft/VAReady2020/blob/master/DemoInstructions/attachingcustomskill.md)
