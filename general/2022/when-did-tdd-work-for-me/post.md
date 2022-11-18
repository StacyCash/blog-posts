# Getting TDD to Work for Me

## Intro

TDD. Test Driven Development. It's kind of like Marmite, a food from the UK that you either [love or hate](https://dictionary.cambridge.org/dictionary/english/marmite). Rarely is there something in the middle.

So it is with TDD. Either people wax lyrical about how great it can be, or they say how useless it is.

Me... I wax lyrical. I've used it often and had some awesome results.

Unfortunately, I've also had some less great experiences and have tried to figure out why I had these failures when using it.

## Adapting Data

An example of where it really helped me was a personal project I was working on. I needed to take data from one data source and transform it into another. Some things were simple "field X => field Y" transformations, others were more complex - having to process data within a field in order to extract the data needed.

I had my requirements and set about creating my tests to ensure that when I gave input to the adapter, it would return what I wanted.

When writing the tests, and sometimes when writing the code needed to turn the current test green, I spotted missing requirements. I added these to my list and worked on them later.

Over the course of a couple of hours I got the 10 or tests passing. I then spent some time playing with the code to see if I could make it more readable for the future. Often going wrong and undoing what I was doing, but always having confidence that I know the state of what I was doing. I had that list of green tests.

At the end of this I ran the application for the first time and... It ran perfectly first time! Awesome!

## Open Source Contribution

Recently I made my first contribution to an open source project and followed the same process. I wanted to add a new feature, and knew what it should do.

The first thing I did was add the tests that I needed to make the feature work. I then started trying to get it actually working.

It took time to get those tests green. And I hated the resulting code.

So I cleaned it up and made it something that, even if I not happy with it, was acceptable to me.

Then I made my PR. The maintainers had some comments on the code, and based on my feature request had done some optimization to existing code (that I had used as a base for my new feature). So I had to make an amount of changes.

Again, it took time, but those tests stayed green each time and I know what I was doing was working.

Then one final comment... Part of the code I made wasn't 100% compliant with the code standards, but it was needed to make the functionality work. It was agreed to disable the code standard or that line and add a comment saying why.

But... I really wanted to make it work right. I racked my brains and had an idea that could work.

And then removed all of my code and started again. Coming up with a new way of solving the same problem that didn't require breaking that rule.

Inside of a couple of hours I had attempt 2 at the solution. Neater, easier to understand and didn't break any code guidelines.

And I knew that it was going to work just as well as the first solution. Because I had those green tests that I could always fall back on. Without those tests there is no way I could have acheived the same result.

The other thing that I could do, because I knew how I was going to test the code, was test from the APi inwards. There is a great talk from [Ian Cooper](https://twitter.com/ICooper) about this [TDD - Where did it all go wrong](https://www.youtube.com/watch?v=EZ05e7EMOLM) which talks about this far better than I can.

But in a nut shell for both problems I was testing the API of the code. Nothing that wasn't used from outside of the functionality was tested directly. That meant that when I cleaned up my code all of my tests were still valid. No brittleness, no rewriting tests to code with the refactor.

## Problems

These are examples of where I have managed to use TDD and get code written, working and maintainable using TDD. And with confidence that I could change it in the future.

But there have also been  times when I've not managed to get into the TDD flow and have been left with worse code, and no safe way to change it. 

And these all have something in common as well. Kind of the opposite of the cases that worked. I *didn't know* exactly how I was going to test. And, if I'm honest, I didn't know how I was going to start developing. So whilst I tried to do TDD, it was too difficult and I didn't.

So... I made a start, worked my way through, and added tests. Generrally at the wrong place, because I was testing tiny bits of code. Rather than the whole functionality. Because I didn't know how to test functionality until afterwards. And those tests were both inadequate and too often aimed at testing the code, rather than the functionality.

## Work in Progress

Right now I am trying a few things to try and get it to work rather more often.

One of things I'm trying is using [spikes](https://www.geepawhill.org/2020/06/02/an-intro-to-spikes/), as descibed by [GeepawHill](https://twitter.com/geepawhill) when things are not clear. The idea is that I allow myself to think with the keyboard, to experiment and try things. No tests, just me, the keyboard and some string language when it doesn't work as I want it to.

But at the end of that thinking with the keyboard the only thing that I take away with me is knowledge. Either knowing what I want to achieve and so I can get my requirements set out better, or knowledge of something that isn't going to work.

None of the code that I produced is taken into production. Rather I have the shape of my solution now, write my tests and then start to work on the solution, test first, in the way that it has worked for me in the past.

This in itself is not easy - the temptation once you are on a path to turn your experiment into final code is really strong!

The second, which sounds so obvious when I type it, is to make sure that I know **how** I am going to test functionality before I start. This has more benefits than just making the coding part easier. And yet this is also one of the harder ones!

This is not an easy process, but the results will be so worth the effort that is put into it!

