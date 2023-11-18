---
title: Contact information in a world post-Twitter
published: false
description: Using the redirect feature of Azure Static Web Apps I set up a redirect to simplify my LinkedIn profile URL so that attendees can still contact me simply after I didn't use my Twitter profile anymore
tags: azure, staticwebapps, linkedin, speaking
cover_image: https://github.com/StacyCash/blog-posts/blob/main/azure/2023/swa-redirect/cover-image.jpg?raw=true
---

The demise of Twitter has hit me in multiple ways...

It was a place where I met a lot of my online friends, where I talked tech with people and (because I did my very best not to get onto the wrong side of it) it was a nice place to spend time.

It was also my primary contact point for the community. I had open DMs (which was not always great) and had some great conversations there with people who I met at conferences, or who saw my content.

These days, I no longer feel that (your mileage may vary, but I no longer like it) and so I spend way less time there.

In fact, the only time I spend there is checking messages. And even then not very often. I need to find new ways of being contacted.

Online I have 3 places where I am present. [BlueSky](https://bsky.app/profile/stacy-clouds.net), [LinkedIn](https://www.linkedin.com/in/stacycash/) and [Mastodon](https://tech.lgbt/@StacyClouds)

The first 2 are the ones where I think that I am best contactable, so those are going to replace Twitter on my slides, along with a link to my [personal site](stacy-clouds.net)

BlueSky is easy, my handle is literally my domain, but LinkedIn is a pain. The URL is long and because of the way LinkedIn search (doesn't) work, you can't rely on the profile name to find it.

So I decided maybe a better way of getting there would be to redirect from my site, and because it's hosted on an [Azure Static Web App](https://learn.microsoft.com/en-us/azure/static-web-apps/overview?wt.mc_id=DT-MVP-5003925) it's also really easy to do!

## Route Management

Azure Static Web Apps have a `staticwebapp.config.json` file that allows developers to control their app from code. This is used for, among other things:

- Authentication/authorization
- Navigation fallbacks
- Setting the runtime for the Azure Function API
- Routing/HTTP Response code overrides

It's this last one that we are going to use today!

By adding the section of code below into my `staticwebapp.config.json` file I could tell the static web app that when someone tries to load [stacy-clouds.net/linkedin](https://stacy-clouds.net/linkedin) it should redirect to my LinkedIn profile

``` json
{
    ...
      "routes":[
    {
      "route": "/linkedin",
      "redirect": "https://www.linkedin.com/in/stacycash",
      "statusCode": 301
    }
  ],
  ...
}
```

With the `route` property we tell the Static Web App what URL to overwrite, with `redirect` we say where it should go, and finally, with `statusCode` we tell the browser that is a permanent redirect.

> There is also an option to redirect if you need to move resources within your own site. Don't mix them up or this won't work 😅

A quick redeploy and  I have a very simple link that I can put on my slides and people will always get to my profile 😊

If you want to learn about the other options, check out the documentation [here](https://learn.microsoft.com/en-us/azure/static-web-apps/configuration?wt.mc_id=DT-MVP-5003925)
