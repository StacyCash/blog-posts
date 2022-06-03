# Developing on an M1 MacBook

Something that has been on my radar for a while is video creation. But there has been a problem.

Actually there have been 2 problems

1. Time. I say yes to too many things, and do sometimes try to take time off...
2. Whenever I tried on my Windows machine using the built in tools it was just a pain and annoyed me

But... I've heard great things about video creation using a Mac and so I decided to treat myself to an M1 MacBook Pro to see if it lived up to the hype.

Then point 1 got in the way, so I still have no idea.

So instead, I have started to use the Mac for other content creation - documents, talks, my book. I can't explain why, but it's just a more pleasent experience to do this on the Mac.

What I hadn't tried to do was set up a development environment, so that was the next on my list.

Coming from a Windows development background to a Mac is a little overwheliming. I am going to write someting on that in the coming weeks (when the book is done and I can spend time on it).

But today... I want to go over the last thing that I was trying to get working. My Azure Static Web Apps, runing using Visual Studio for Mac and the SWA CLI tool.

No matter what I did it just would not work. The Azure Function would not pick up the local.settings.json and so couldn't access my CosmosDB. I checked I had it in the right place, that I had formatted the JSON correctly. Checked that I had spelt the name of the file right. 

Nothing. 

And nothing online about MacBooks having issues Azaure Functions.

Hours, and hours were spent with me pulling my hair out because this **should** work and I want to get it working.

Today I fixed it.

The problem...? 

I forgot to set the proerties of the file when I created it and it was never being copied to the output folders. Doh!

On the bright side, it works now and I have another choice of development machine when I want to do some hobby development!