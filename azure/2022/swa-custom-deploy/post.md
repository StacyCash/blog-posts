---
title: Taking Azure Static Web Apps from Out of the Box to Your Complex Pipelines
published: false
description: 
tags: SWA, Azure, CICD
cover_image: https://raw.githubusercontent.com/StacyCash/blog-posts/main/azure/2022/swa-custom-deploy/cover-image.jpg
---

Earlier this year at [AzureLive](https://azurelive.nl) I gave a talk on authentication in Azure Static Web Apps (SWA). Before my talk I was speaking with someone who thought that SWAs were fun, but not something that you could use seriously. The biggest complaint they had: the build process.

Out of the box you get a CI/CD flow set up for you. Every push to your trunk branch will trigger a build and deploy. And you don't need to do anything to make this happen. Awesome!

But whilst this does work for simple applications, and for getting people started, if you have a large and complex application - and your SWA is only a small part of that - then how can you run all the processes that you need to?

By this they meant things like:

* How do you run your unit tests?
* If deploying to multiple environments, how do you ensure that the same code is always being deployed?
* How do you take control over **how** the code is built, when it's all encased in a magic GitHub action?

For the first of these there is a cheat if you still run a small application - simply build the solution and run your unit tests **before** you use the GitHub action. This works, it's what I was doing at the time for my personal website. But it also adds build time to the deploy process that I would rather not have to wait for if building anything serious.

The other two... Well, SWAs come out of the box with support for staging environments - but again, whilst this works really well for smaller applications, I can see an app that fits into a larger eco system would be a bit more complex.

And the last... It's a closed system. You supply the code. The GitHub action figures out how to build it. That's it.

Seems that they had a point. But I wasn't going to give up that easily. So... Challenge accepted!

## Out Of The Box

Let's start with an out of the bog Azure Static Web App GitHub Workflow Job:

```json
build_and_deploy_job:
if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
runs-on: ubuntu-latest
name: Build and Deploy Job
steps:
    - uses: actions/checkout@v2
    with:
        submodules: true
    - name: Build And Deploy
    id: builddeploy
    uses: Azure/static-web-apps-deploy@v1
    with:
        azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_AMBITIOUS_GROUND_011396E03 }}
        repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
        action: "upload"
        ###### Repository/Build Configurations - These values can be configured to match your app requirements. ######
        # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
        app_location: "Client" # App source code path
        api_location: "Api" # Api source code path - optional
        output_location: "wwwroot" # Built app content directory - optional
        ###### End of Repository/Build Configurations ######
```

So what does this do?

* It's triggered when a push occurs on the branch triggering the workflow
* It checks out the repository
* It uses the `Azure/static-web-apps-deploy@v1` action to do the following
  * Build the app, using the code in the `app_location` directory
  * Builds the Azure Function app, using the code in the `api_location` directory
  * Deploys the app to the Azure Static Web App

How it does this, we don't know or care - it just happens. And 99.9% of the time it works and we never have to think about it.

However, if you want to do something more advanced, you can do it. We can tell the Action not to do some of these things. In order to do that we need to look at some options that don't exist out of the box.

## Customizing the Action

Let's customize that action to only upload the application to the SWA.

```json
- name: Build And Deploy
id: builddeploy
uses: Azure/static-web-apps-deploy@v1
with:
    azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_YELLO_RIVER_13413E103 }}
    repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
    action: "upload"
    ###### Repository/Build Configurations - These values can be configured to match you app requirements. ######
    # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
    app_location: "ClientDist/wwwroot" # App source code path
    api_location: "ApiDist" # Api source code path - optional
    skip_app_build: true
    skip_api_build: true
    ###### End of Repository/Build Configurations ######
```

On the surface, this looks very similar, but there are some differences:

* The App Location has changed to "Client/wwwroot"
* There are 2 new options
  * `skip_app_build`
  * `skip_api_build`

These 2 options are self-explanatory. If you set them to `true`, then the action will skip the build of the app. If you set them to `false`, then the action will build the app.

So we are no longer letting the Action build the app. We simply give a location where the Action can get hold of the built application. This could be an app that has been built, and tested in previous steps.

Or it could be an app that has been built in a previous job, allowing us to deploy the same compile application to multiple environments.

## Using This in Real Life

So... You take what I have said, and you use it in your own application.

When you do this the first thing you will notice is that you API calls, if you are using them, will fail.

Oops. It turns out that that Action does more than simply build and deploy. It also analyses the source code and sets up the SWA accordingly.

As it's no longer building the API, it can't do that. Is it deploying .NET? NodeJS? Who knows.

Well, we do, and by bypassing the Action we need to manually tell the SWA what it is that we are doing.

As with most configuration for an SWA, this is done in the `staticwebapp.config.json` file.

In the snippet below I've set the SWA to run .NET 6.0 as the API runtime:

```json
  "platform": {
    "apiRuntime": "dotnet:6.0"
  },
```

By setting that at the top of the config file, our API should start working again when it's deployed 😅

## Conclusion

So... SWAs are both awesome for beginners, who just want the ease of deployment out of the box without having to worry about *how* it actually happens and for developers with more complex workflows that want full control.

In this way we can incorporate SWAs into larger, more complex systems where we need full control to ensure that our apps are behaving as they should do. 

Checkout the [MS Docs](https://docs.microsoft.com/en-us/azure/static-web-apps/build-configuration?tabs=github-actions) for more information on how to configure the Static Web App workflow.

Cover photo by [Lucas Santos](https://unsplash.com/@_staticvoid?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/complex?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
