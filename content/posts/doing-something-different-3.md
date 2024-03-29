---
title: "Something Different #3 - Go"
date: 2023-08-15T09:09:12+01:00
draft: false
icon: 🧑‍💻
---

The second thing I did, was learn to code in Go<!--more-->


As with games, I have a bit of a history with coding, especially certain types of software. In previous jobs I mostly used Ruby and JavaScript (and a little TypeScript) with a pinch of Python and PHP to wield various automated test frameworks or create internal websites to host useful test tools.

For some time I had a hankering for a language that was a little stricter without being oppressive and Go seemed to fit that nicely. I'd also dabbled in Go a little over the years and was keen to use it more thoroughly. More on the features and philosophy of the language and my feelings about it [later](#the-go-programming-language).


### The Plan

Here my plan was a little different. Instead of focussing on creating a couple of prototype games where the product was the goal and the tooling a little more incidental, this time I would be focussing on gaining a good understanding of Go - the resulting output was less of an immediate concern.

To this end I did something I've never done before in learning a programming language. I picked up a book. Or rather I borrowed one from a good friend. The Go Programming Language (Alan A. A. Donovan and Brian W. Kernighan, 2016).

My knowledge of Ruby and JavaScript was mostly gleaned from the necessity of a particular task at a particular point rather than setting out with an idea to take a [different and more structured approach to the learning](#the-different-learning-approach). 


### How It Went

I really, really enjoyed this. Perhaps because it was a little closer to my experience than games development, and perhaps because at heart I enjoy writing code - I'm not entirely sure, but it definitely grabbed me.

I worked my way through The Go Programming Language, taking time to type out and understand the examples given. Typing out rather than copy-pasting helped me to develop muscle memory for common language patterns and made it much easier to write my own code later without having to check back for specific syntax. I think ```if err != nil {}``` is probably burned into my brain tissue by now.

Over the next few weeks I graduated from smaller demo scripts for particular features like channels and websockets to creating slightly larger (although still simple) projects of my own. The culmination of this was four web-based applications:

1. A web app, lovingly named 'BinJuice', which calculates which bins will be collected in my area and on what day, and displays it with slightly more CSS animations than are necessary. This is now running full time on the household Raspberry Pi alongside PiHole and has proven quite useful.
2. An API using the Fiber framework and an SQL database which stored and retrieved information about items from the game 'Vampire Survivors'.
3. An API using the Fiber framework and an SQL database for a tech task to store, retrieve, update and delete vehicle information with some logicical constraints (such as vehicle age) across multiple tables in a relational manner.
4. A URL shortener, allowing you to create a shorter link for sharing (along the lines of TinyUrl or Bitly) either via the simple HTML page or an API endpoint.

After the initial foundation into Go from my book learning, these tasks pushed me to create my own projects from scratch and interact with some popular Go packages like http and sql, as well as the Fiber web framework. Much like error handling, setting up routes and handling responses with SQL queries was now more familiar.

I am absolutely never going to claim that I 'know' a language, or that I even know how much I know about a language. These weeks spent on first book learning and then creating my own projects though have given me confidence that I both enjoy coding outside automation, and can do it.


### Learning and Thoughts

#### The Go Programming Language

Exploring Go, I realised that its design philosophy mirrors much of my own feelings about what code and software should be. 

Code should be simple, clear, readable and predictable. If it takes an extra line or two, or a slightly longer variable name then so be it. I can spare the extra bytes.

I also like languages where there is a near-universal accepted approach to many common situations. I refer to ```if err != nil {}``` as one example amongst many. When this is the case, reading other people's code is easy, and not an exercise of understanding a never-before-seen syntax. It emphasises the role of code as a means to solve problems, not as an end in itself.

In the same way, Go's good core library allows a standardisation and predictability to code and results that seems hard to achieve in languages which lack a deep core library and leave it to the community to develop multiple solutions to the same problem. While I can see this would encourage creativity in some cases, this is set against unpredictable outcomes and competing standards for almost the same requirements.

Compared to Ruby and JavaScript, on the whole I find I like the greater confidence I get from compiled and statically type-checked languages. At least in my experience it ensures I write better code up front, and vastly reduces unexpected errors during use of the code later on.

Oh and I like the Go gopher too :)


#### The Different Learning Approach

Something I've realised over the years but never applied that much to coding is that I learn really well from books, more than I do from online materials like posts, courses and videos. I don't totally understand why but I think my brain reads and absorbs information from printed pages at a much more sensible pace, whereas decades of computer and Internet use have trained me that a computer screen means 'skim until you identify one nugget of information, then get out'.

Alongside this, by starting from a wider overview of the language and systematically working through a book, I feel I was able to get a better understanding of all the tools and features that were available to me to solve problems. Skimming blog posts and targeted online solutions I find can lead to quite 'spiky' learning, where knowledge is good in one area but there is no overall idea of the breadth of the language you are using.

The second thing I found during this period was that I greatly appreciate not having to rush. 

Almost all my previous coding as part of a job was done in a hurry, with numerous other tasks (often required, not often useful) piling up in the background. The speed-at-all-costs nature of many areas of modern e-commerce made learning extremely fragmented and often superficial.

In much of my work on Go skills this time I was able to read about, experiment with and actually _understand_ what I was looking at by the time I moved on. This holds more value for me than copy-pasting from Stack Overflow to find a quick solution before the next meeting, which neither I nor anybody else would easily be able to debug in the future if needed.

Where time permits, I would definitely learn in this way again, although I suspect my chances of doing so while 'on the job' might be more limited. It certainly made me appreciate having the time to have no goal but to learn, rather than read one thing to solve one problem while being bombarded with Slack messages.

### Conclusion

I found so many things I liked in this chapter. Well, some I knew I liked but had lost some of my enthusiasm for over the years.

Firstly, if I have to learn a larger topic then I find books to be preferable to online courses - at least initially. No doubt the latter are useful but the ability to set my own pace and take a wider view of the topic over 'learn X in 24 hours' felt beneficial.

Secondly - and connected with the firstly - disconnecting learning from an immediate problem to solve, and learning merely with the goal of obtaining knowledge to apply to future currently unknown problems, was a nice change and removed a lot of the pressure. If I was interested or thought an area could be useful, I would explore it without guilt and as a result I believe learned more.

Thirdly, I get on extremely well with Go so far. It provides what I'm looking for in a reasonable learning curve, with enough support to find solutions if I'm struggling and most importantly a philosophy of simplicity and clarity.

Finally, I rediscovered a love of coding. When I first moved from manual testing into writing automated tests, it was like a world opened up before me as I realised I had the ability to do so much. Over the subsequent years I think my horizons narrowed as I was pushed by time constraints and speed demands to only create the bare minimum automated testing without thought for longer term improvements or creative approaches.

Unbinding my experience of coding as a means to create automated tests and tools, and opening it out to be a much more general skill to solve problems with, allowed me to start having ideas again and create from passion and excitement rather than obligation.
