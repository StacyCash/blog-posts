# Azure Static Web Apps CLI - API Options

Last week I was presenting at [CloudBurst](http://cloudburst.azure.com), talking about one of my favorite subjects: Azure Static Web Apps!

At the point of demonstrating how to run the application locally, it kind of went wrong...

The CLI just would not pick up the Azure Functions on a different port to the default of 7071. After trying a few things to solve it on stage, I gave up and just changed the port that Visual Studio was using to host them. A great short term solution, but of course I needed to let the audience know what I did wrong so that they could learn from my mistake.

This is the command I was using. See if you can spot my mistake faster than I did!

``` ps
swa start https://localhost:7837 --api-location 7133
```

The problem... I used the wrong argument to specify the location of the Azure Functions. There are two ways to solve this problem

I could have specified the full URL to the Azure Functions with the `--api-location` argument

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

Let's start with the API location. This can be used in two ways:

- Building and running the code directly
- Connecting to an existing Azure Functions instance

### Building and running the code directly

By using either a relative or absolute path, you can tell the CLI where to find the Azure Functions code. It will use the Azure Function Core Tools to try to build and run the code inside of that directory.

Starting the SWA CLI using a relative path:

``` ps
swa start https://localhost:7837 --api-location ./api
```

And using a full path:

``` ps
swa start https://localhost:7837 --api-location C:\code\swa-app\api
```

My main use case for this is when I want to just run the application without debugging it - I generally add the `--run` argument to build and run the front end as well.

### Connecting to an existing Azure Functions instance

This is a little less common in my experience (yours may differ 😅), but it can be useful. You can use the `--api-location` argument to connect to an existing API endpoint.

This can be useful if you are connecting to something other than an Azure Function, or want to connect to an existing function instance.

For example, if I am working with an App Service Web Api rather than an Azure Function, then I can start my SWA CLI pointing the API location to the running application by using the URL of the local development service

``` ps
swa start http://localhost:5001 --api-location http://localhost:5094
```

If I am connecting to an existing, deployed Azure Function then I can use the URL of the deployed function

``` ps
swa start http://localhost:5001 --api-location http://localhost:5094
```

## --api-port

The other option that I mentioned (and the one that I should have used in my demo 🫣) is the `--api-port` argument.

This does not change the location of the 

// Used in conjunction with --api-location and running code

// USed in conjunction with --api-location connected to a development server

// Used without the --api-location
