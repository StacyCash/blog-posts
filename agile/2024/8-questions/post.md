---
title: 8 Questions to Help You Stay Safer
published: false
description: Can you safely take on a new feature? These 8 questions will help you to ensure that you can.
tags: 
# cover_image: https://direct_url_to_image.jpg
# Use a ratio of 100:42 for best results.
# published_at: 2024-03-11 15:28 +0000
---

On 17th October I gave a talk to [DevOps Days Amsterdam](https://www.meetup.com/nl-NL/devopsamsterdam/) about experimentation and failures that we had at [Omniplan](https://omniplan.nl/). Of course just talking about failures is not completely useful, more useful was what we learned from the experience. One of the topis was about the "8 Questions" that we now ask ourselves before we start work on a new feature.

After the talk someone asked for a link to the 8 questions, "Sure!" I said, "I have a blog post about it". But it turns out that whilst I meant to write one up, I never did. Oops 🫣😅

> **Important Note:** These are our 8 questions. Some will be relevant to other people, some not. This is not supposed to be a one-size-fits-all solution. It's a starting point for you to build your own questions that are relevant to your team and your work.

## Why we started the questions

We started the questions because we saw that some changes were not thought through as well as they should have been. That we didn't quite have a grasp on the size of the change, or the impact it would have. That we didn't have the safety net in place to ensure that we could make the change safely. Nothing too bad, but it wasn't the direction we should have been moving in, and things took longer than we wanted as a result.

However... We didn't want to introduce a standard checklist "Definition of Ready" that would be a tick box exercise (and grow each time something unforeseen happened). We wanted to ensure that we were thinking about the right things at the right time, and that we were all on the same page. And thats what these questions are supposed to be: something to make us stop, think, and discuss before we start work.

## The TL;DR;

Honestly, I think that just looking at the questions without the context is not going to be very useful. But if you are in a hurry or need a reference, here they are:

1. Why? Does everyone understand why we are making this change?
2. How are we going to prove that it works, with actual test cases before we start?
3. Which of these tests should be ran manually, and what should be automatic checks?
4. What can we break when making this change?
5. Do we have the correct automatic regression tests to catch it if we do?
6. Technically, how are we going to approach solving the problem?
7. Do we need major refactoring in order to do so?
8. Team Check In: Do we have consent from the team to move forward?

### Why? Does everyone understand what problem are we solving with the feature?

Developers are not just code monkeys. We are there to solve users problems. That's something I have believed since I was at the start of my journey at University, and it's something that I still believe now.

As such, "Because that's what the spec says" should never be an answer to the question of why are we building this.

There are multiple issues here:

- You don't know if you are solving the problem, or dealing with symptoms
- You don't know if this is the best way to solve the problem
- You don't have any "buy in" to the solution, and so are less likely to be motivated to do a good job

Much better to know what the problem is, and why we are solving it. I've had it multiple times in my career when digging for the why from the business actually found a route cause that was much easier to solve than the original problem. And provided a better solution for the user as well!

### How are we going to prove that it works, with actual test cases before we start?

"How am I supposed to test, when I don't know what I'm building?" is a common question. And it's a good one. But, as with the why above, it likely means that we haven't got deep enough into the problem.

We have a problem to solve, which means we have an end state. Are you going to know all of the tests at this point? No. Some are going to appear as you work. But there should be a success state, and fail state, that we can describe before we start. At least one of each - and likely more than one!

Make sure that you know this, as a team, before you start. Chances are that doing this is going to provide more value than just getting tests! This is where you can start to work through the problem as well!

### Which of these tests should be ran manually, and what should be automatic checks? (note: this is not about unit tests)

Don't automate all the things. Test automation has a cost associated with it. The cost of writing the automation, the chances of that flow changing and the test no longer being valid or even the time taken to execute the test not being worth the extra confidence that test gives us.

Some tests are going to be important to ensure that we have solved the problem as we hoped to, whilst not being a test that is required for each and every release.

As such it's important to make sure that we know, before we start to write code, which tests we want to manually run before we make our pull requests, and which we want to run each and every time we deploy our application.

As a team we need to make sure that we find the happy medium between automate everything, and not having confidence that we can safely change our code without manual tests before it goes to production.

### What can we break when making this change?

Things rarely happen in isolation. We have a complex system, and when we make a change there is a reasonable chance that it could impact other functionality. By having a service oriented architecture, and using onion architecture inside of those services, we try to limit the things that we can break. But we can still always break things.

So before we start to make changes we need to know what else may break in the process so that we can keep an eye on it.

#### And do we have the correct automatic regression tests to catch it if we do? (note: this can be, but isn’t limited to, unit tests)

Once we know what we can break we have an extra question

> Will we know if it has broken?

Because our current automatic checks are not always as good we would like.

This question goes deeper than simply asking "is there a test for this line of code". There can be checks in place, but if those checks don't exercise the code as you expect then they are not going to give you the safety net that you hoped for.

So, do you understand the code that can break? If not you need to make sure that you do. 

Once you have that understanding, you can check what the tests are doing and if they are running through the possibilities well enough to know if something has broken after your change is complete.

#### If not, what do we need to add?

And when we see checks that are missing, we need to ensure that we create them.

Before we start to actually work on the code.

In a completely separate PR even.

This is for 2 reasons. The first being that we want to keep the PRs as simple and atomic as possible. This PR will simple be adding tests, with no functional changes.

The second is that you want to know that these tests are working before you start your own work.

### How are we going to approach solving the problem?

Now that we have that safety net in place we can start to really look into how we are going to solve the problem itself.

How are we going to implement the solution? What options are available to us? What patterns could help us?

Most importantly: how are we going to solve this as a team, and not just a collection of individuals working at the same metaphorical island of desks?

Here again, we may spot things that we missed in an earlier stage and have to rewind a little. That's fine, it just means that we are improving our understanding all the time.

### Do we need major refactoring in order to do so?

There is a wonderful quote from Kent Beck:
> First make your complex change simple. Then make your simple change

And... There is something of a misnomer here. There are two distinct processes that fall under this question, and we need to ensure that we know what we are doing. It can have a big impact on the risk!

Refactoring: taking code and shaping it so that it's easier to maintain, extend and, if needed, change in the future. In theory we shouldn't be changing code here. Simply altering the location of the code being called.

Rewriting: Taking functionality and reimplementing it in a way that allows better testability, extension and maintenance in the future. Sounds similar, but here we are not just moving code around to improve it. The actual implementation is changing as well. The functionality should stay the same to the outside world, but the way that it works may bear no resemblance. Doing this may have more impact, but also adds a lot more risk to the process.

Neither of these is better than the other. Use whichever one is required, just make sure that you yourself know what your plans are before you start.

#### Which we can only do after ensuring we know what we can break

And, yes, this comes **after** the missing checks to existing code have been made. Should we need to refactor then we want to know that we have not broken anything again!

And remember that those tests should be in a PR on their own. If you have to change tests for your rewrite because the structure is fundamentally changing then make sure that those tests you create are one level higher so there are still untouched tests proving that worked previously, works now. This is especially important with the rewrite as the chance of changing tests is higher.

### Do we understand, and agree with the changes that we are going to make?

We are getting close now...

We know why we are making a change, we know that we can make it safely - both for the new functionality and the things that we could break in the process. We know how we want to approach it.

An important question that remains is:
> Do we all agree that we are doing the right thing?

Because if we are not in agreement it's going to make the change very interesting to actually make.

Now... This is not supposed to be a question to quiet dissent, or force people to agree to something they don't.

It's to ensure that we have checked that we are not missing something. That we have considered options in how we are going to solve the users problem.

And get different perspectives that we can maybe use should our original idea not work out as we hoped 😵‍💫

### Can we split it into stories so that we can make a comparative estimation of the tasks against each other?

Finally. We need to know roughly how long something is going to take. Not to hold teams to account should things not go according to plan, but to allow communication outside of the team for when functionality is going to be available.

1 giant, 3 month feature/story is hard to manage. 12 smaller ones are much easier. And when things are not going well we can alert people to the delay sooner.

How can we split a story to provide some value at each step and still keep it small enough to watch progression during a sprint, and across multiple?

## Conclusion

This looks like a lot of work. It is. Certainly for the short term when we have a lot of tests and refactoring that we need to do.

However... In the long term it should get less and less, we should start to see that we do have the correct coverage to ensure that old functionality still works after we have completed our changes. We should have less serious refactoring to do to ensure that we can safely add our new functionality.

This doesn't mean that there will be no refactoring that we need to do. Just that it will be less, and simpler. Hopefully 😅

But the most important thing is that we work ahead. This isn't something that can be done during sprint planning, or when a story or task is picked up. This is something that happens over time. These questions take place at different times during the refinement of a feature or story from the vague "we want to try something", to the "these stories show how we are going to do it".

It's not easy, it never is - but the understanding, safety and confidence in what we do will increase with it.
