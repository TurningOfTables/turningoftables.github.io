---
title: "Planespotting"
date: 2023-09-13T10:53:13+01:00
draft: false
icon: ✈️
---

A Go app to show nearby planes <!--more-->

### The initial idea

Actually it wasn't really my idea. I came across another implementation of a planespotting app in JavaScript using the OpenSky API and thought, "I will do that but in Go". Then I did a bit more searching and it turns out there are tons of these.

Undaunted, I wanted to make it anyway because it combines two things that I like: planes and Go.

I had some idea of the basic requirements up front:

- be able to specify a location you're at
- be able to specify a radius in which you want to be notified about planes
- send an OS notification when a plane was 'spotted'

As usual, I knew that this was likely to grow a little as I had ideas during development - and it did a little!


### Writing, Iterating, Refactoring

After initially writing the basic functionality above without too much trouble, I added on a couple of neat (at least to me!) features. The first was the ability to feed config in from outside the app, so you didn't have to specify it each time and it would be easier to set up for other users. The second was saving 'progress' of some sort - this culminated in a list of the flight numbers and a total of how many planes you've spotted. Keeping a list of flight numbers also prevented the same plane being constantly 'spotted' as it stayed in the area nearby; especially obvious if your location is set at or near an airport.

Once I had these in place, I decided the app was getting big enough to need a bit of splitting out. I created sub-folders with packages of 'helpers' for everything outside `main.go`. So I had `helpers/save/save.go` and `helpers/config/config.go` and `helpers/formatters/formatters.go` etc., each with their own tests such as `helpers/save/save_test.go`

This worked just fine, and in fact I rather liked splitting the code into 'systems'.

### Adding the UI

What happened next was I decided I wanted to add a UI, and this proved harder than expected. I used the [Fyne](https://fyne.io/) and found it to be simple to pick up and create functional and decent looking APIs. However it was tricky to integrate into my previously written (and structured code).

The UI needs to run from main - all good so far. The UI also needed to interact with other areas of functionality in the helpers - again, no problem. However the helpers _also_ needed to access back into main in order to update the UI on changes such as status, or saves, which was hard to do - going back _up_ the tree, as it were.

So what did I do in the end? I moved much of the code back out of their own sub-folder packages, and instead just split it into files in the root of the project as part of the main package. So `helpers/save/save.go` with `package save` became `/save.go` with `package main`.

This allowed easier access between the different sections of the apps, while I kept packages that didn't need to push info back into the UI in `helpers/` (namely, the `formatters`). Overall I did solve the problems, although it required significantly more work than I expected.

On reflection, my mindset was probably used to building an API which can then be universally consumed by a front end client. In this case though, since I hadn't really built an 'API' to be 'universally consumed', when it came to adding a consumer it was tough going.

### What I would do differently

There are two main lessons I can take from this about how I write more code into projects.

#1

My code needs to have more cleanly defined boundaries, and be written to be consumed cleanly and more agnostically. Different functionalities should be better split out. [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns)

In general this was less of an issue in my smaller earlier projects, but the larger they get the more this becomes something I need to manage better.

#2

Clearly I will never know all of the requirements and features of a project before even starting to write it. However, adding in the UI was a fairly major turn - I think if I'd decided on this significant part earlier on then it would have saved a significant amount of pain later. I should try and decide on the *large* pillars or requirements before starting, even if additional smaller items are added in later.

### Conclusion

This was a super useful project in that I had to confront a few things I hadn't done before. I got deeper into configuration, saving and retrieving files, and also dabbled into creating my first basic UI with the Fyne framework.

I'm also fairly pleased with the end result in terms of functionality. The code would certainly benefit from a little more tidying and documentation, but a user can run the binary, enter their details and be getting planespotting notifications in just a couple of minutes. 🎉

[Check it out on Github!](https://github.com/TurningOfTables/planespotter)