---
title: Back to streaming! Stream 2024-03-06
published: true
description: An overview of my first stream of 2024, and my plans for the coming months.
tags: dotnet, streaming, health
cover_image: https://raw.githubusercontent.com/StacyCash/blog-posts/main/streaming/2024/Stream%2020240306/cover-image.jpg
# Use a ratio of 100:42 for best results.
# published_at: 2024-03-06 14:19 +0000
---

After a long time away I finally managed to make it back to streaming today. It felt... Great. But also exhausting!

Which meant that it was also very short, and I saw that what I thought of as OK planning, really wasn't - lesson learned for next time!

## Recap

Here is a recap of what I did today!

## Where have I been the last 12 months

The last time I streamed was in NDC London with Amy Kapernick. That was more than 12 months ago!

Unfortunately, it was just after that that my long-covid totally grounded me. No work, streaming, coding for pleasure, or talks for most of the year.

I'm slowly adjusting to the new normal. I have some good days and some bad. I am slowly getting back into the community, from speaking at meetups, conferences, and MCing.

And starting the stream again today, even though it is not a "good" day, felt great and seemed a good next step!

## Plans for the coming months

Over the coming months, I am planning on a stream every 2 weeks. Hopefully, that won't be too extreme for my health, but will be frequent enough that I can achieve things that I want to. Fingers crossed...

I have a number of projects that I am going to be working on live on stream:

- Rebuilding the .NET SDK for my domain provider that I started before I was ill
- making a package to make simple SVG graphs - something that I need for work, and want to remake the first graph I ever coded back in 2000!
- Showing what can be done with [Azure Static Web Apps](https://learn.microsoft.com/en-us/azure/static-web-apps/?wt.mc_id=DT-MVP-5003925) - not only to help me write the 2nd edition of my book but also to look at the more advanced features!
- Building a reference app of some kind using lots of different Azure resources, and asking for help from my friends in the community to help with things that I'm not an expert in

## Awful code

Finally, I opened a project that I hadn't touched since I became ill. The current implementation for accessing the API of my domain provider.

It was so old that my new machine couldn't even build it - I didn't install .NET 7 on my new machine.

I wanted to do this as much as a warning to others as anything else. That application was built as temp code. Something that I could use for my Static Web Apps in the Enterprise talk whilst I finished it off.

There is no such thing as temp code. Once you are using it, it becomes production code. Seeing as I have a version that does work for my talk I am considering killing the current code and starting again from scratch - build it properly, and when it gets to parity with what I use in my talk, I'll replace the code there with this one.

At least I could use the stream time to update all the NuGet packages and get it running on .NET 8.0 😅

That's all I had for this stream - actually, I was about asleep by the time I finished - so see you in 2 weeks to actually start to do real coding!
