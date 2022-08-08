---
title: Sometimes you need to take a step back
published: true
description: The story of me pulling my hair out for no reason when trying to get a MacBook Pro to run Azure Functions (hint: it was my fault 😅)
tags: development, mistakes 
cover_image: https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1xjgw6wn0dzqjcr1xpgm.png
---

Before the summer treated myself to a MacBook Pro for video creation. I didn't get around to trying it for that purpose yet, but I have used it for writing content and quite like it.

Seeing as I had it available, I thought I'd try to see what development was like on the machine.

Coming from a Windows development background to a Mac is a little overwhelming. I am going to write something on that in the future (when the book is done and dusted, and I have some free time on it).

But today... I want to go over the last thing that I was trying to get working. My Azure Static Web Apps, running using Visual Studio for Mac and the SWA CLI tool.

It was a nightmare!

No matter what I did it just would not work. The Azure Functions would fire, but would not pick up the `local.settings.json` and so couldn't access my CosmosDB container to read data.

I checked I had it in the right place, that I had formatted the JSON correctly. Checked that I had spelt the name of the file right.

Nothing.

And nothing online about MacBooks having issues Azure Functions. If there is nothing there, then it can't be a problem on the platform... Someone would have noticed by now.

Maybe a setting that people developing on these machines just know about and I was getting lost?

Hours, and hours were spent with me pulling my hair out because this **should** work, and I really want to get it working.

Today I fixed it.

The problem...?

I forgot to set the properties of the local.settings.json file when I created it and it was never being copied to the output folders. Doh!

On the bright side, it works now and I have another choice of development machine when I want to do some hobby development!
