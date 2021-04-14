---
title: Making your first Azure Static Web App with Blazor and Azure Functions
published: false
description: Deploying a Blazor WASM application, with an Azure Function API to an Azure Static Web App (Preview)
tags: 
//cover_image: https://direct_url_to_image.jpg
---

## Blazor

With the introduction of Blazor we had the ability to write SPA web applications using the same technology that we wrote our server side code.

In fact, for those using Server side Blazor it can run alongside our server side code!

But, as well as Server Side Blazor, the announcement also included Client Side Blazor - the ability for our app to run in the users browser via wasm.

That is, on the first call a wasm compiled .Net runtime is downloaded to the client, along with our code, and ran inside the browser.

## Static Web Apps

If the code runs inside the browser, then we don't need a full blown web server in order to host our application. We can simply serve the files to our users. This makes our life much simpler!

Previously we could do this with an Azure Storage Account - setting it up to be a static web application.

Now there is a dedicated resource for this! Albeit in preview right now...

Now inside of one resource we can host not only our client application for delivery ona  global scale, but also have an API hosted as an Azure Function along side to give us a globally distributed, fully scalable application!

### Deployment

When the Azure Static Web App preview first came out, there was one choice for hosting our code: GitHub.

When you created the app you connected the resource to our GitHub repo, and the Azure Portal would create a deployment Action for you. Another benefit! Out of the box you have a flow for continuous deployment of our app out of the box. Including a workflow to help you with pull requests, and checking our code in a production like environment before pushing to production.

If you didn't have a GitHUb account though, you had a problem! Sorry...

That changed around April 2021 - support for other ways of hosting our repo was introduced. However, the integration, right now, is not on the same level as GitHub, and there are more manual steps you need to complete.

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

Before we can create our Azure Static Web Application we need a Blazor application to deploy into it.

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

Visual Studio should now create our client application. If you have never created a Blazor application before then run the application and take a look around 😀

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

In the scaffolded application there are two demo pages. One shows how to interact with the pages (Counter.razor), the other shows how to retrieve data from an external source and iterate it to the screen (FetchData.razor)

It is `FetchData.razor` that we are going to be changing for this demonstration.

By default the data is fetched from a static JSON file created inside of the `wwwroot` directory, we are going to change this JSON call to call our Api

1. Open the `FetchData.razor` page
2. On line XX replace the call to `sample-data.json` with `api/weather-forecast`

```c#
// TODO: Put code sample here
```

### Change the HttpClient when Debugging

But wait! We said that the Api would be on a different port? So where do we get that from?

We are going to add a local settings file, something that won't be pushed to GitHub, so that when we run locally we can tell the application to look somewhere else for the data.

1. Create a `local.settings.json` file in the `wwwroot` folder
2. Add a value into file `API_LOCATION`, with the value `https://localhost:7071/`

Your `local.settings.json` should look like

``` json
{
  "API_LOCATION": "https://localhost:7071"
}
```

### Add the API URL for Debugging

Now that we have the URL, we need to use it!

When the application first loads a http client is created for the dependency injection. This is set, as standard, to the base address of the application.

That is what we want when running in our Azure Static Web App, but not when debugging, there we need to use the URL stored in our `local.settings.json` file

1. In the `Client` project open `Program.cs`
2. Replace line 20 with the code snipper below

``` C#
// TODO: Add code snippet for program.cs file here
```

This code will check if there is an environment setting called `API_LOCATION`, and if there is use that rather than the Base URL of the application itself.

### Add the WeatherForecast function

We now have a client application that will call the API when we need it to, but as yet there isn't a function to serve the request.

We'll build this now

1. Right click on the project file for `Api`
2. Click `Add`
3. Select `Function`
4. Select `Http Trigger`
5. Call the new function `WeatherForecastFunction`
6. Change the `Run` function signature as follows

``` C#
//TODO: add code snippet for run
```

> This sets the function to be get only, sets the route for the function to be `weather-forecast`, and the return type to an IEnumerable of WeatherForcast

7. Add the code to define the `WeatherForecast` struct

``` C#
//TODO: Add weatherforecast struct here
//TODO: Check to see if this is actually needed, or can we use dynamic objects here...
```

> Normally we would put this object in a separate file, and share the model between the `Client` and `Api`.

8. Add the code to generate the results which we are going to return to the body of the `Run` function

``` C#
//TODO: Add code snippet for generating weather forecast
```

Our finished function should look like this:

``` C#
//TODO: Add weatherforecast class code here
```

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

Stop the application - we just have one more change to make before pushing to GitHub!

## Finishing Up

We can debug the application, and run it in production, but we have one step left to make it work well for our users.

Because we have built an app to be hosted in a Static Web App there is no web server sitting behind it - just static files. That's what we want! But it also comes with a downside...

All routes on our application exist only in the browser when the application runs. We can visit the route of the site, and click through to a page (the URL may change, but there are no server requests made). What we can't do is go directly to page without first visiting that index page. When we try that the server tries to find the page that we are looking for, fails - because it doesn't exist - and returns a 404 error.

Not what we want...

Thankfully there is a simple solution to this. Ensure that there is a fallback route in set-up in for the site. The Static Web App will use this to redirect pages which it can't find.

1. Add a new file to the `wwwroot` folder called `Routes.json`
2. Paste this JSON snippet into the file

``` json
{}
```

This file matches all routes not found on the server (with the `/*` route)
These routes are redirected to `index.html`, the front door to our site
And the status is overridden as a 200 - otherwise our new pages would be found, but the response code would still show an error

On the client when this redirect happens it picks up the redirect and tries to open that route inside the application. If it is found we see the page, otherwise we see the client 'Not found' page.

As we are running our application inside of Visual Studio this isn't something that we can show locally - so we will test that this is working inside of Azure

Now our application is ready for deploying - let's check in out code, push it to GitHub and get started on create our Static Web App in Azure!

## Create the Azure Static Web App

We have an application ready to deploy, now we can make the Azure Resource to deploy it.

It's time for us to open up the portal!

### Create the Resource Group

The first thing that we need to create a resource group to hold our resources

1. Click the resources link
2. Click the add button
3. Check that the subscription is correct
4. Give the Resource Group a name
5. Select the region that best suits your location, I'm based in the Netherlands, so I picked "West Europe"
6. Click "Review and Create"
7. If the validation passes click "Create"

A resource group should take a few seconds to provision.

When it does click on the "Go to resource" button

### Create the Static Web App

We now have an empty resource group, time to put something in it

1. Click the "Add" button
2. In the search box type `Static Web App (preview)`
3. Client the link //TODO: Check the actual link
4. Click Create
5. In the screen that opens, check the subscription and resource group are correct

> If you create a new resource from the a resource group directly then these should be automatically filled, but checking is always recommended

6. Fill in the name of the Static Web App, unlike a 'Web App' resource, this does not have to be unique inside of Azure
7. Select 'GitHub`

> As mentioned at the start of this tutorial, GitHub isn't the only way to deploy a Static Web App, but it's the easiest at the moment - so we are using it here.

8. Click `Authorise`

> A second window will open, log into GitHub with the credentials needed to access your repo 

9. Select the organisation, repo and branch that our Blazor/Azure Function app has been pushed to
10. In the drop down lost of deploy profiles select 'Blazor'
11. Check that the "Client" and "Api" input fields are set to the location where our Client and Api are stored

> In our example app we created the projects with the names "Client" and "Api" so that we can use the default values here. If yours are in a different location you will need to make a change to reflect that in these fields

12. The output folder can be anything as long as the folder does not exist in the repo. Leave it as default unless you have a 'wwwroot' in the root of your repo
13. Click 'Review and Create'
14. If the validation passes click 'Create'

The new resource should be available in a few seconds

### Check new Resource

### GitHub Actions

## Next Steps

## Further Reading

[Azure Static Web Apps](https://azure.microsoft.com/en-us/services/app-service/static/)

[MS Docs - Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/overview?WT.mc_id=AZ-MVP-5003925)

[MS Learn - Static Web Apps](https://docs.microsoft.com/en-us/learn/paths/azure-static-web-apps?WT.mc_id=AZ-MVP-5003925)
