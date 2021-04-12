---
title: Making your first Azure Static Web App with Blazor and Azure Functions
published: false
description: Deploying a Blazor WASM application, with an Azure Function API to an Azure Static Web App (Preview)
tags: 
//cover_image: https://direct_url_to_image.jpg
---

## Blazor

With the introduction of Blazor we had the ability to write SPA web applications using the same technology that we wrote our server side code.

In fact, for those using Server side Blazor it can run alongside your server side code!

But, as well as Server Side Blazor, the announcement also included Client Side BLazor - the ability for your app to run in the users browser via wasm.

That is, on the first call a wasm compiled .Net runtime is downloaded to the client, along with your code, and ran inside the browser.

## Static Web Apps

If the code runs inside the browser, then we don't need a full blown web server in order to host our application. We can simply serve the files to our users. This makes our life much simpler!

Previously we could do this with an Azure Storage Account - setting it up to be a static web application.

Now there is a dedicated resource for this! Albeit in preview right now...

Now inside of one resource we can host not only our client application for delivery ona  global scale, but also have an API hosted as an Azure Function along side to give us a globally distributed, fully scalable application!

### Deployment

When the Azure Static Web App preview first came out, there was one choice for hosting your code: GitHub.

When you created the app you connected the resource to your GitHub repo, and the Azure Portal would create a deployment Action for you. Another benefit! Out of the box you have a flow for continuous deployment of your app out of the box. Including a workflow to help you with pull requests, and checking your code in a production like environment before pushing to production.

If you didn;t have a GitHUb account though, you had a problem! Sorry...

That changed around April 2021 - support for other ways of hosting your repo was introduced. However, the integration, right now, is not on the same level as GitHub, and there are more manual steps you need to complete.

For that reason we are going to use Github today! A post for Azure DevOps is in the pipeline, but lets start with the simplest option!

With that - let's start!

## Prerequisites

This tutorial is going to be step by step - taking you through each action we need to do to get an application created, and deployed into Azure. There are a few things that we are not going to cover here though:

* GitHub: I'm assuming that you have
  * A GitHub account
  * An empty repo setup (with a Visual Studio `.gitignore`)
  * That you have this repo cloned to your machine

If not then this would be a good time to bookmark this page and [set it up](https://docs.github.com/en/github/getting-started-with-github)

I'm also assuming that you have an Azure account. We will be going through the steps of making the resources that we need in the tutorial, but not for creating the account itself.

You can find instructions for creating a free account [here](https://azure.microsoft.com/en-us/free/)

When the GitHub repo has been cloned, and the Azure account is ready - let's get started!

## Making Our Application

The first thing that we need is an account to 

### Making the Client

Inside of Visual Studio 2019 latest version (community, professional or enterprise editions will work)

1. Create a new project
2. Search for a Blazor WASM Project
3. Click Create
4. Set up the details as follows
  * Project Name: Client
  * Location the directory that contains your GitHub Repo directory (If your repo is in `c:\code\my-github-repo` then enter `c:\code`)
  * For the solution name enter the name of your GitHub repo (in our example above `my-github-repo`)
5. Select .Net 5.0
6. Leave the options as default

* [x] Set up for HTTPS
* [ ] Hosted .Net Core Application
* [ ] Progressive Web Application

7. Click create

Visual Studio should now create your client application. If you have never created a Blazor application before then run the application and take a look around 😀

### Making the API

So far we have our client side Blazor application, and as is we can deploy a static site using just this project.

But we want to have a dynamic site! So we need somewhere to get the data from - our Api!

1. Right click on the solution in the solution explorer
2. Click `Add`
3. Click `New Project`
4. In the "New Project" pop-up search for `Azure function`
5. Click `Next`
6. Give the project a name `Api`
7. Click `Create`
8. Select `HTTP Trigger`
9. CLick `Create

> If you get the option to pick a framework version select .Net Core 3.1 - .Net 5.0 isn't well supported yet!

Visual Studio should now scaffold the Api for us and add it to our solution

## Setup Debugging

So, now we have a client application, and an API to get data.

Inside of a Static Web App in Azure the client will be able to make HTTP calls to the API without an extra work (aside from the code to actually make the call of course). It does this by putting a reverse proxy behind the URL which can direct the call to either the client or the Api.

Unfortunately, locally we don't have that luxury and so we need to do a little more work if we want to debug on our machine!

> The Static Web App CLI ias just been released in preview which can also help here, but that will be covered in another blog post!

### Set the Start-Up Projects

The first thing that we need to do is ensure that both of our projects will run when we debug the application. By default only the client will be ran, so we need to set the start up projects.

1. Right click the solution in the solution explorer
2. Click `Properties`
3. In the screen that opens click `Multiple Startup-Projects`
4. In the list of projects ensure that both are set to 'Start'
5. Click 'Save'

### Use the API in the FetchData page

### Add the API URL for Debugging

### Change the HttpClient when Debugging

### Add the WeatherForecast function

### Allow CORS for Local Development

The last step that we need to debug locally is to allow allow cross origin requests when running in our development environment.

Yes, cross origin! Our client will be running on one port, our Api on another - and that's not allowed out of the box for security reasons!

1. Inside the `Properties` folder of the `Api` add a new file: `launchSettings.json`
2. Put the following json in the new file

```json
{}
```

Now when the Api is launched locally in VisualStudio CORS will be enabled for all calls.

### Check out Application is Running

With these steps done we can now run our application locally!

Run the application, and open the developer tools of your browser. Open the network tab and wait for the home page to load.

Now clear the list of files (you don't have to do this step, but it reduces the noise for the next step) and click 'Fetch Data'

In the network tab the call to the API should now be visible - if everything is working rather than the call to the `example-data.json` file, we should now see the call to `localhost:7071/weather-forecast`.

Stop the application, and push the changes to the GitHub repo. We are now ready to make our Azure Static Web Application.

## Finishing Up

## Create the Azure Static Web App

### Create the Resource Group

### Create the Static Web App

### Log into GitHub

### Check new Resource

### GitHub Actions

## Next Steps

## Further Reading

[Azure Static Web Apps](https://azure.microsoft.com/en-us/services/app-service/static/)

[MS Docs - Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/overview?WT.mc_id=AZ-MVP-5003925)

[MS Learn - Static Web Apps](https://docs.microsoft.com/en-us/learn/paths/azure-static-web-apps?WT.mc_id=AZ-MVP-5003925)
