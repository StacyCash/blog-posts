# My First Performance Tests

Question: Is this going to be a tutorial or a story
Question: Focused on getting started with K6, or actually looking at the results
Question: Include the mind numbing work to remove everything around the performance problem (to see that it wasn't a problem after all)

This week I've spent a lot of my time working on a really strange performance issue.

One of our processes uses an external plugin to generate documents and is a little slower than we would like. So at the start of this week I began playing with [K6](https://k6.io/) to see what I could find.

Firstly, K6 is awesome! We had some scripts created by a performance tester over the summer and using those gave me an instant start for the test I wanted to write.

Running the test locally I couldn't actually see any issue. 

