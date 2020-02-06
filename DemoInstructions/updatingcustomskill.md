# Updating your custom Skill
aka.ms/VAReadyDemo4

## Develop your language understanding model
45. Navigate to https://preview.luis.ai/ and click on the app named after the Skill you deployed: _"{Azure resource name}en-us\_{Skill name}"_
1. Create a new [Intent](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-concept-intent)
1. Add utterances that you want to handle with that Intent
1. Click to `Train` and `Test` your app
1. Once you're ready to continue, click to `Publish` to production

## Update your local custom Skill
50. In a PowerShell Core window, navigate to your custom Skill's directory and run:
    ```
    ./Deployment/Scripts/update_cognitive_models.ps1 -RemoteToLocal
    ```


## Develop your dialog
51. In Visual Studio, open the Skill's _Dialogs/MainDialog.cs_ class
1. In the `RouteStepAsync()` method, add switch-case statement to handle your new Intent
1. Inside the new case, send a message in response to the user:
    ```cs
    await stepContext.Context.SendActivityAsync("<RESPONSE_MESSAGE>");
    return await stepContext.NextAsync();
    ````

1. Save your changes and press `F5` to start the Skill locally
1. Open the Emulator to test the local custom Skill
1. Click `create a new bot configuration` and enter the following:
    1. **Bot name**: Custom Skill
    1. **Endpoint url**: http://localhost:3978/api/messages
    1. **Microsoft App ID**: Copy-paste the "microsoftAppId" from the Skill's `appsettings.json`
    1. **Microsoft App password**: Copy-paste the "microsoftAppPassword" from the Skill's `appsettings.json`
1. Click `Save and connect` to run your bot
1. Test an utterance you trained in LUIS to see the new response message returned locally

## Publish and update the Virtual Assistant connection
59. [Update your custom Skill's manifest](https://microsoft.github.io/botframework-solutions/skills/tutorials/customize-skill/csharp/3-update-skill-manifest/) (we will skip this for now - waiting for more documentation to be released.)
47. In your custom Skill solution in Visual Studio, right-click and **Publish** the project again

1. Once publishing is complete, navigate to `Test in Webchat` to see your updated Skill running in Azure
1. In a PowerShell Core window, navigate to the Virtual Assistant project directory 
1. To update the Virtual Assistant with the changes you made to the Skill, run the following command:
   ```
   botskills update --remoteManifest "http://<SKILL_AZURE_NAME>.azurewebsites.net/manifest/manifest-1.1.json" --luisFolder "..\..\<SKILL_PROJECT_NAME>\<SKILL_PROJECT_NAME>\Deployment\Resources\LU" --languages "en-us" --cs
   ```
   Once that completes, your local Virtual Assistant can now route your new trained utterances to the custom Skill
1. Open the Virtual Assistant in the Emulator again to test your new utterances from LUIS
1. In the Virtual Assistant solution in Visual Studio, right-click on the project in the Solution Explorer window and select **Publish**
1. Once publishing is complete, navigate to `Test in Webchat` to see your updated Virtual Assistant running in Azure

---

# Some next steps

- Create bot responses using [Language Generation](https://github.com/microsoft/botbuilder-dotnet/tree/master/doc/LanguageGeneration)
- Connect your Virtual Assistant to the [Power BI Template](https://microsoft.github.io/botframework-solutions/solution-accelerators/tutorials/view-analytics/1-intro/)
- Enable [Continuous Integration](https://microsoft.github.io/botframework-solutions/solution-accelerators/tutorials/enable-continuous-integration/csharp/1-intro/) and [Continuous Deployment](https://microsoft.github.io/botframework-solutions/solution-accelerators/tutorials/enable-continuous-deployment/1-intro/)
- Participate on [GitHub](https://github.com/microsoft/botframework-solutions/issues)
- [Adaptive Dialogs](https://github.com/Microsoft/BotBuilder-Samples/tree/master/experimental/adaptive-dialog)
