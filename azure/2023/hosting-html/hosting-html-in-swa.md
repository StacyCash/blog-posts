---
title: Hosting HTML in Azure Static Web Apps
published: true
description: Setting up a pipeline for hosting plain HTML files in an Azure Static Web App
tags: azure, swa, learning
# cover_image: 
# Use a ratio of 100:42 for best results.
# published_at: 2023-01-25 14:38 +0000
---

At a recent event I was discussing Azure Static Web Apps with a friend of mine and we were talking about hosting plain HTML files inside of an SWA.

I know the theory, but it's not something that I had actually done. So let's look at what we need to do to make this work.

Assuming that the repo containing the file looks something like this

``` txt
/
- wwwroot/
  - index.html
```

OK, a fairly small site - but the deployment remains the same not matter how big the site is, as long as all the HTML files are located underneath the `site` folder.

In order to deploy plain HTML files we need to stop the build pipeline from performing the build step - after all there is nothing to build.

If we change the build and deploy step in the GitHub workflow as below the `Azure/static-web-apps-deploy@v1` action won't try to build the source code, it will just deploy it. Exactly what we need here.

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
    app_location: "wwwroot" # App source code path
    skip_app_build: true
    ###### End of Repository/Build Configurations ######
```

But this assumes that you already have a pipeline, so when creating the Azure Static Web App that you want to convert from a build to HTML. So let's look at how we can create one from scratch.

For this we are going to use the Azure Portal

In a resource group, click on the `+` icon to add a create a new resource.

[!Create a new resource](https://)

- Search for the Azure Static Web App
- Click create
- Fill in the standard details
- Select the Repo branch to deploy

When selecting the type of application to build to select Custom

Then do something else 😅
