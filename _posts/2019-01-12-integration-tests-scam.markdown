---
layout: post
title:  "Notes - Integration tests are a Scam"
date:   2019-01-12 17:00:00 -0700
categories: notes testing
---
I watched a very interesting video on a flight home last week:

<iframe width="560" height="315" src="https://www.youtube.com/embed/VDfX44fZoMc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Since I just read [Make is stick](https://www.amazon.ca/Make-Stick-Science-Successful-Learning/dp/0674729013)
this is my attempt at active learning. Just going to ask myself questions and try to explain concepts from the video in my own words.

What is an integration test? Where you're testing more than one thing, or testing differnt bits of interesting behavior.
A test where if something breaks, its not easy to know where the problem exists.

What are unit/collaboration tests? Tests that do one thing and one thing only. A test where if it fails, you know
exactly where and what the problem is. The idea of a collaboration test is that its from the point of view from the client.
Does the client interact properly.

Why should we value unit/collaboration tests over integration tests? Simpler unit tests help us put pressure on the
design more. When smaller pieces we're building with are hard to test, we know there is a design problem.
Where as an integration test is not putting this kind of pressure on design. We're testing larger parts and
seeing less of the internal problems. TDD is not about testing, its about your design.

Integration tests take a lot of setup and a lot more effort to maintain. When you're trying to do an integration tests,
coming up with all the test cases for multiple systems can create a combinatoric (worse that exponential!) number of test
cases. It's impossible to write all the cases for our integration tests. Also, integration tests can take a long time to run!
Where as we can have thousands of smaller unit tests running in a second.

Proper unit and collaboration testing means you'll end up creating almost a ring architecture of tests (more like
an onion). Each level the the ring represents a layer of communication and collaboration you need to test on both
sides. If you create mocks that mock one layer, you need to make sure those expectations are tested on the other side.
Eventually you will reach the outer part of the ring where you are testing things like direct DB access. And you should
be doing your best to minimize these slow tests using simple design techniques. When you use this ring architecture
approach to testing, you turn the combinatoric numer of test cases into just a linear progression. (Turn multiplication
into adding). Also just writing less integration tests leaves you more energy to write smaller more resillient collaboration
tests.

My thoughts? - A few intergration and smoke tests to run through all your systems can add some value. It's nice to know all
parts of the system are reachable and working. But this would probably be really simple tests that just test really simple
endpoints. But you don't want these kinds of tests to get too out of hand.
