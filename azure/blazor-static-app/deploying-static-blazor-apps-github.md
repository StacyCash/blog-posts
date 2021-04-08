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



## Getting Started

### Github Repo

### Clone the Repo

## Making Our Application

### Making the Client

### Making the API

## Setup Debugging

### Static Web App CLI

### Use the API in the FetchData page

### Add the API URL for Debugging

### Change the HttpClient when Debugging

### Add the WeatherForecast function

### Allow CORS for Local Development

### Check out Application is Running

## Finishing Up

## Create the Azure Static Web App

### Create the Resource Group

### Create the Static Web App

### Log into GitHub

### Check new Resource

### GitHub Actions

## Next Steps
