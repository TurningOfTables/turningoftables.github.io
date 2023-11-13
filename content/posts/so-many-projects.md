---
title: "So Many Projects #1 - Wires"
date: 2023-11-13T09:25:55Z
draft: false
icon: 📑
---

Working further with Go, and creating a microblog.<!--more-->

I realised I hadn't posted an update in a while, and even if nobody reads these then it's nice for me to have a record of what I've been doing.

I now have about ... 14 Go projects on Github, and I haven't actually given a rundown of more than a couple - what each one does and the area
that it helped me to learn. I've been a bit sidetracked by life (and a nice holiday!) recently but wanted to get these down before the end of
the year.

I won't go heavily into the code here, and a few aren't really tidy enough to make public yet, but you should get an overall impression of
what functionality each one has.

### Wires

#### Functionality

Wires is a microblog built with [Fiber](https://gofiber.io/) and [Gorm ORM](https://gorm.io/). At this point I'm relatively used to Fiber and continue to find it a nice solution for
apps which need a tiny bit more than fairly simple routing, which the [Go net/http package](https://pkg.go.dev/net/http) provides.

You can register, log in, log out, post, view other people's lists of posts, change your password, delete your account and switch between profile pictures.

### DB and ORMs

Wires is backed by my usual simple SQLite database, although of course in a real use case you'd certainly want to change this to Postgres or similar.

Gorm and other ORMs I find myself falling in and out of love with, sometimes within the same day. On the one hand it's nice to have a programmatic
way of building up SQL (and might have saved me from a typo in another project's raw SQL which took me an hour to find), and coupling structs to
database models without having to update the SQL makes iterating quite a bit easier. No need to handle migrations and such. On the other hand it does
make me feel as though I'm spending time learning an ORM rather than adding functionality by just writing SQL, and potentially adds in
another layer of complexity or source of issues to debug. Overall my feeling is that if you use an ORM, you have to adopt it wholeheartedly and couple
it tightly to your project. You have to take the leap, use it early on and see the benefits as your project grows in size.


One of the parts I learned from in this project was implementing a notion of authenticated and unauthenticated pages - or some that were partially authenticated like viewing a user's
list of posts. In this latter instance I wanted anybody to be able to view a user's posts, but only that user to get the form to add another post (and ensure you couldn't
just post directly to the API anyway). Mostly this was a logic problem, as well as a few forays into Fiber's [Locals](https://docs.gofiber.io/api/ctx/#locals) which 
were particularly handy here, using bcrypt to hash and verify passwords.

While there are some optimisations I can make to the number of DB calls, overall I'm reasonably happy with this as a first pass.

### The Front End

In this case I didn't use any specific front end framework or solution, and instead opted to use the templating provided by Fiber (which is identical to the
text templating in Go). While this was a little bit of a throwback to my Ruby on Rails days in some ways when using partials, once you tear your 
mind away from the component patterns of modern JavaScript apps it's a perfectly effective way of building an app. Plus I always have an innate bias for using
core functionality where I can, in preference to additional dependencies on third party libraries.

Front end testing is implemented via a series of Playwright tests alongside the project, and basic styling is added via Bootstrap.

### Conclusion

Although the idea behind the project (microblog) wasn't exactly revolutionary, it served the purpose of allowing me to venture further into some more complex
authentication and routing scenarios, as well as some heavier use of templating and thinking carefully about the logic and passing data around a web app more
effectively.

Developing this project further would likely involve the following:

1. Email rather than username signup, requiring integration with an SMTP service or external auth/SSO handler.
2. Optimisations in how many database calls are made for authentication, as these could eventually cause heavy load.
3. Switching to a non-file-based database solution for better performance at scale.
4. The ability to customise your own 'Home' page with people you follow, and of course allow blocking of user content.
5. Ability to upload your own profile picture.

### Screenshots

![Wires Profile Page](/wires_1.png 'Wires Profile Page')
![Wires Home Page](/wires_2.png 'Wires Home Page')