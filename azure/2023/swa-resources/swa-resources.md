---
title: Azure Static Web App Resources
published: false
description: A selection of Azure Static Web App Resrouces
tags: azure, swa, learning
cover_image: https://raw.githubusercontent.com/StacyCash/blog-posts/main/azure/2023/swa-resources/cover-image.jpg
# Use a ratio of 100:42 for best results.
# published_at: 2023-01-25 14:38 +0000
---

I adore Azure Static Web Apps! I've been using them since they were in preview, and my site is built and hosted on one 😊

I love the simplicity in setting them up, I love the fact that out of the box they provide so much functionality without the user having to be an expert, and I love they are affordable for people to be able to try them out

## Resources

I've written a few talks about static web apps and here you can find a list of resources that can help you in your journey

### Beginning Azure Static Web Apps with Blazor

I'm going to start with the shameless plug... Last year I spent a lot of time and energy writing a book to guide you though creating an application using Blazor and .NET functions.

The book guides you though creating the application, deploying it using the Azure Portal and GitHub actions, how to debug it locally and using the Azure Static Web App inside of the application.

You can find the book on [Amazon](https://www.amazon.com/Beginning-Azure-Static-Web-Apps/dp/1484281454), and other book sellers

### Microsoft Learn

This training path is an awesome resource if you are getting started with Azure Static Web Apps. It covers the basics of hosting static files, how to connect an API, and authenticating users. A perfect place to start!

Rather than being .NET focused, this path covers many different languages

[MS Azure Static Web Apps Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-static-web-apps/)

### Azure Static Web App Documentation

To help you in your journey there is some great documentation available for Azure Static Web Apps covering both basic and advanced functionality. To progress further in your journey these resources are invaluable

You can find the documentation [here](https://learn.microsoft.com/en-us/azure/static-web-apps/)

### SWA CLI

THe SWA CLI started life as a way to help the developer inner loop. One of the awesome things with an Azure Static Web App is that it "glues" the front end and back end together so that they appear to the world as one single application.

When running locally though, that glue isn't there. Before the SWA CLI was available in preview there was a lot of code needed for application to know if they were running inside Azure or not so that the front and back end could still communicate. And if authentication was used there was no way of testing this locally. The SWA CLI provided a NodeJS server that pretended to be that Azure Static Web App, so applications could be ran locally exactly<sup>1</sup> the same as in production.

<sup>1</sup> I say exactly, it's not **exactly** (the tool tells you this when you run it), but it's close enough for most work outside of custom authentication testing

Once it was released GA though, the amount of functionality increased greatly! The SWA can now be used for initializing an SWA, deploying, logging into Azure and more.

You can find the documentation [here](https://azure.github.io/static-web-apps-cli/), and the tool itself is open sourced and can be found [here](https://github.com/Azure/static-web-apps-cli)

### az staticwebapp CLI

Last on the list is the `az staticwebapp` CLI. Extending the power of the `az` CLI with Static Web App specific functionality. Using this tool you can provision new Azure Static Web Apps, and manage environments settings, secrets, hostnames (custom domains) and much more.

When using using Azure Static Web Apps in a more professional environment (and not just clicking in the Azure Portal) it is an important tool!

You can find the documentation [here](https://learn.microsoft.com/en-us/cli/azure/staticwebapp?view=azure-cli-latest)

## Notes

These are all resources that I use when working with Azure Static Web Apps. if you think that anything is missing or could be improved please feel free to reach out to me on [Twitter](https://twitter.com/stacy_cash), [LinkedIn](www.linkedin.com/in/stacycash), or [Mastodon](https://tech.lgbt/@StacyClouds)
