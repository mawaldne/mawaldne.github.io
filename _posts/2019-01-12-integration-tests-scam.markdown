---
layout: post
title:  "Notes - Integration tests are a Scam"
date:   2019-01-12 17:00:00 -0700
categories: notes testing
---
I watched a very interesting video on a flight home last week:

<iframe width="560" height="315" src="https://www.youtube.com/embed/VDfX44fZoMc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Since I just read [Make it stick](https://www.amazon.ca/Make-Stick-Science-Successful-Learning/dp/0674729013)
this is my attempt at active learning. I'm just going to ask myself questions and try to explain concepts
from the video in my own words.

What is an integration test? An integration test is where you're testing more than one thing or
testing different bits of interesting behavior. It is a test where if something breaks it's not
easy to know where the problem exists.

What are unit/collaboration tests? These are tests that do one thing and one thing only.
They are tests where a test failure tells you exactly where and what the problem is. The idea of
a collaboration test is to look at behavior from the point of view from the client, and
ask: “does the client interact properly?”

Why should we value unit/collaboration tests over integration tests? Simpler unit tests help us put pressure on the
design more. When smaller pieces we're building with are hard to test, we know there is a design problem.
Where as an integration test is not putting this kind of pressure on design. We're testing larger parts and
seeing less of the internal problems. TDD is not about testing, its about your design.

Integration tests take a lot of setup and a lot more effort to maintain. When you're trying to write an
integration tests, coming up with all the test cases for multiple systems can create a
[combinatorial growth](https://en.wikipedia.org/wiki/Combinatorial_explosion) of test cases.
It's impossible to write all the cases for integration tests. Also, integration tests can take
a long time to run! Where as we can have thousands of smaller unit tests running in a second.

Proper unit and collaboration testing means you'll end up creating almost a ring architecture of tests (more like
an onion). Each level the the ring represents a layer of communication and collaboration you need to test on both
sides. If you create mocks that mock one layer, you need to make sure those expectations are tested on the other side.
Eventually you will reach the outer part of the ring where you are testing things like direct DB or 3rd party library
access. You should be doing your best to minimize these slow tests using simple design techniques. When you use
this ring architecture approach to testing, you turn the combinatorial growth of test cases into just a
linear growth. (Turn multiplication into adding). Also just writing fewer integration tests leaves you more
energy to write smaller more resillient collaboration tests.

My thoughts? - A few intergration and smoke tests to run through all your systems can add value.
It's nice to know all parts of the system are reachable and working. These should be just a few
simple tests that just test really simple endpoints.

