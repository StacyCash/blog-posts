# Azure Static Web Apps CLI - API Options

Last week I was presenting at [CloudBurst](http://cloudburst.azure.com), talking about one of my favroutie subjexcts: Azure Static Web Apps!

I was giving my quick tour talk. In 60 minutes we go from having no application, to building a Blazor WASM application, with an Azure Function API, deploy it to a new Azure Static Web App and then add authentication.

One of the steps in this process is showing how to run the application locally.

For those unformiliar, when you deploy an Azure Static Web app you build static files with make up the front end. These can be anything from a static site using plain HTML, to a dynamic application using a SPA framework of somekind.

If data is needed for the application then this can be created using Azure Functions in either .NET or Node.js.

And then there is the glue of the Azure Static Web App that joins these two seperate processes together so that they appear to the outside world as one single system. Without the developer having to connect things up themselves.

Great when running in Azure, but you don't want to deploy your application each and every time you need to debug something 😅

Enter the [Azure Static Web Apps CLI](find this link) (SWA CLI). Whilst this doesn't give us an Azure environment locally, it does allow us to pretend that we do 😊

So what went wrong in the demo during my talk?tlak to the 

Well... When I tried to run the applcation locally I could not get the CLI to pick up the correct port for the Azure Functions

``` ps
swa start https://localhost:7837 --api-location 7133
```

Some of you may notice the problem already, I didn't until after the talk was finished - rather I changed the port that he Azure Functions use to the default for the SWA CLI so that I didn't need to specify it when running the application

``` ps
swa start https://localhost:7837
```

A great short term solution, but of course I needed to let the audience know what I did wrong so that they could learn from my mistake.

The problem was that I used the wrong argument to specify the location of the Azure Functions. There are two things that I could/should have done differently

I coulld have specified the entire path to the Azure Functions

``` ps
swa start https://localhost:7837 --api-location http://localhost:7133
```

This would have worked. But it's maybe overkill for what I needed. There is a simpler way

``` ps
swa start https://localhost:7837 --api-port 7133
```

This simply redirects the port to a different place than de the fault `7071` that the SWA CLI uses.

> This *used* to be the default for .NET, but it was changed to use random port recently.

So... That was my mistake. But let's use it as a learning opportunity! Let's look in detail at what these command line arguments can give us!

## --api-location

Let's start with the API location.

// running code directly

// Conneting to a development server

## --api-port

// Used in conjunction with --api-location and running code

// USed in conjunction with --api-location connected to a development server

// Used without the --api-location
