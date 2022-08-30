# Getting TDD to Work for Me

## Intro

TDD. Test Driven Development. It's kind of like Marmite, a food from the UK that you either [love or hate](https://dictionary.cambridge.org/dictionary/english/marmite). Rarely is there something in the middle.

So it is with TDD. Either people wax lyrical about how great it can be, or the say how useless it is.

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

So I cleaned it up and made it something that, if not happy with, was acceptable to me.

Then I made my PR and the maintainers had some comments on the code, and based on my feature request had done some optimization to existing code (that I had used as a base for my new feature). So I had to make an amount of changes.

Again, it took time, but those tests stayed green each time and I know what I was doing.

Then one final comment... Part of the code I made wasn't 100% compliant with the code standards, but it was needed to make the functionality work. It was agreed to make sure that the reason needing to work around the coding standards should be added.

But... I really wanted to make it work right. I wracked my brains and had an idea that may work.

And then removed all of my code and started again.

Inside of a couple of hours I had attempt 2 at the solution. Neater, easier to understand and didn't break any code guidelines. And this was doable because I had those green tests that I could always fall back on.

## Problems

These are just two examples of where I have managed to use TDD and get code written, working and maintainable using TDD. And with confidence that I could change it in the future.

But there have also been many times when I've not done this.

I could not think how I wanted to test what I was doing, I couldn't figure out how I wanted to build my code and, well sometimes I guess I just wanted to write it.

Even when I knew I had the examples that worked, I didn't work it the right way.

Or I tried to work it the right way, and just stared at the screen not sure how I wanted to start.



## How I'm trying to improve

[Spikes](https://www.geepawhill.org/2020/06/02/an-intro-to-spikes/)