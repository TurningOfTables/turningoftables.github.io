---
title: "The Boy Scout Rule, Or Not"
date: 2024-06-08T09:32:08+01:00
draft: true
icon: 😇
---

It's common to have both new features and tech debt competing for your time. What do?<!--more-->

I think this is something most coders must have come across at some point. On the one hand you have new features which need implementing, but you're also aware of continuing improvements and tech debt that needs addressing within your codebase. Enter...

### The Boy Scout Rule

> "Leave the code cleaner than when you found it."

The way I interpret this is that you don't go out of your way to address large areas of tech debt as a specific task, but you tidy up with small improvements as and when you come across issues during your other work. 

See a typo? Fix it. See an older approach or library being used that's not the current standard in the rest of the code base? Switch it over. You need to make sure you don't get pulled into wide-ranging, blanket improvements that would significantly slow you down, though.

I like this approach in many ways. It's easier to plan in a continuous stream of iterative changes, and their small size reduces the risk of each individual alteration. That being said, there are dangers and downsides which I've noticed recently.

Firstly, you inevitably end up with a bit of a **mixed code base** - especially when some of your boy scout changes are to switch from one pattern or library to another for a specific purpose. As an example, you might be switching from one test assertion library to another. Following this rule, there could be an extended period when your code contains both old and new libraries - in fact if there are areas of code that don't get updated, they could potentially remain on the old library for a long time.

Secondly, you need to **know when to stop**. It's extremely easy to fall down rabbit holes where one tidy-up leads to another, which unearths another area of the code that needs a *whole heap* of changes. Before you know it, your PR has grown to touch dozens more files and the original change or feature is dwarfed by the resulting tweaks. I try to follow the principle of not going beyond files that I was changing anyway, but this can be hard to achieve when the initial change ricochets around your repo

Finally, and leading nicely on from the point above, these small iterative improvements can be **unexpectedly risky**. Now I get to sound smart by saying: "Chesterton's Fence". Originally from a 1929 book by G.K Chesterton, this is the principle that "reforms should not be made until the existing state of affairs is understood". To paraphrase his example heavily: you may come across a fence across a road. Unless you know why it's there, don't remove it.

Although his subject matter was very different, many people have adapted this idea into working with existing software. You may come across some apparently poorly written code as you tidy. Unless you understand the reason why it was written this way originally, be _very_ wary about changing it. This is true at any time, but especially so when making incidental tidy-up changes during another task.

In conclusion, I still favour making these 'boy scout' changes while working. They're a good way to at least reduce the accumulation of tech debt that often accompanies fast, feature-led development required for many modern applications. When employing the rule though, it's important to **be careful** about your changes. Without boundaries and proper consideration, they can have unexpected consequences on the consistency of the overall project, the time taken to reach goals and release features, or introduce unexpected issues with areas of code that are not the current focus of thought or testing.


