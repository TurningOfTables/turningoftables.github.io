---
title: "Choosing an Automated Test Framework"
date: 2023-01-01T13:08:48Z
draft: false
---

When deciding on a framework or tool for automation, there are a dizzying array of possibilities. There are certainly no right and wrong answers - but an outline of what to consider might look like this.<!--more-->


### Who Will Use It?

Think very carefully about the skills and knowledge of the people who will be using the framework. This is especially important if you are leading a team and making a decision about technology used by less experienced team members. Try out candidate frameworks for yourself and consider the learning curve as well as the depth of training materials available. Get less experienced team members to test the learning process and see if they find it approachable before you commit.


### Is It Well Established and Actively Maintained?

Particularly in the world of web development, frameworks of all kinds come and go constantly. Many new contenders appear with slick .io websites promising incredible things, while only achieving the basics before fading away.

On the other hand, well established frameworks and tools tend to have better documentation, more community support and are more 'battle hardened'. They tend to be less buggy and more predictable to use.

You may be investing significant time into writing code or tests using the framework. Is the project likely to continue to be around and relevant for years to come? If the framework stagnates or is abandoned it can potentially leave you with slowly degrading tests as web technology changes. Although you can't always accurately predict this, you can make sensible bets on frameworks with large, active communities and responsive development teams.

Additionally, be alert for signs that your current framework may be in trouble such as slower rates of updates or mounting issue reports which go unacknowledged.


### What's Beyond the Basics?

Many frameworks will initially seem good as the journey to your first test is made as smooth and seamless as possible. You might be able to write a test that navigates to a website and clicks a button almost instantly, but think further beyond this.

How flexible is the framework to meet your specific needs? Does it support use cases that might be harder to implement, like iframes or shadow DOMs? How reliably does it wait and can its assertions be extended? How configurable is it, and can you fill in gaps with your own code easily? 

Try to think about the hard and fiddly tests against slow, unreliable or badly engineered software, not just Hello World.


### And What's Beyond the Tests?

Plan where the framework is going to fit into any other requirements you might have, past the tests themselves. Can it be run as part of a pipeline? What reporting outputs does it support, or will you have to write your own?


### Summary

To sum up, there are countless frameworks which can make writing simple tests easy. What differentiates them is deeper than that - the learning curve, the support and updates, the ability to extend it and shape it to your needs, and its integration options.