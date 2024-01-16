---
title: "Generics and HackerRank"
date: 2024-01-16T09:49:05Z
draft: false
icon: ⬆️
---

A recent Go addition, and a new area of learning<!--more-->

Coming from mostly loosely typed languages like JavaScript, the concept and usefulness of generics was a little bit new to me. I'd seen numerous older posts and answers decrying the lack of generics in Go, and also learned that they were now a feature of the language. In the first part of the post I use the go.dev site's examples and explanation to walk through how I understand them.

Alongside this, I've changed the type of learning I've been doing again and been exploring HackerRank - a site that presents various code challenges and checks your solutions, which then earn you points and ranks. In the second part of the post I talk about how I've found it, what I think has been useful, and what is perhaps not so relevant.

### Generics

With strongly typed languages, it's common to run into a scenario where you want to apply the same change to two different types. 

The example used by go.dev is that of having two maps. One a `map[string]int64` and the other a `map[string]float64`. Normally when you want to perform the same action on two different types - such as adding together all the values - you likely have to write two different functions. One to sum a `map[string]int64` and the other to sum a `map[string]float64`.

Naturally this leads to a bit of code duplication, as the body of each function is essentially the same and only the function signature changes to reflect the different types.

With generics it's possible to write one 'generic' function that allows you to sum either type. 

I'm going to skip the first iteration of how to implement these from the docs as I find the last solution much tidier and extendable.

In our case we want our function to allow either `int64` or `float64`. You can create an interface to act as your constraint like so:

```
type Number interface {
    int64 | float64
}
```

You can then create a function like this which sums anything that follows the constraint of `Number` (example taken from go.dev)

```
func SumNumbers[K comparable, V Number](m map[K]V) V {
    var s V
    for _, v := range m {
        s += v
    }
    return s
}
```

I won't go into this in too much more depth here, because the actual doc pages on it already explain it well, but this gives a quick idea of what generics do, the problems they solve and how they're constructed. For further reading I encourage you to check out [the full post on go.dev](https://go.dev/doc/tutorial/generics)

### HackerRank

As I've been learning, my pattern of coding has generally gravitated towards writing with a particular purpose in mind. Whether that's spotting planes, creating a micro-blogging site, or knowing when my bins are being collected. Overall I am in favour of this type of learning and coding, because it reminds us that (usually) coding is to solve a problem.

Alongside this though, it can be difficult to find time to practice coding skills without setting out a long period of time in which to bootstrap a project and do a lot of building before even getting to learn something new. This is where I've found HackerRank (and similar tools) to be a useful aid.

The general idea is that you are presented with a code challenge - often to write just a single function which, when tested, gives the expected outputs for the test inputs. It leads to a slightly different way of thinking in that the overall goal of the project matters less, and instead it polishes your skills at manipulating data, performing mathematical operations, and often iterating on your function to improve performance.

So what have I learned from this that I didn't pick up from fuller project creation? It's a good question. I think it forces you to focus in on smaller units of code, and perhaps most of all hones logical thinking approaches to coding. I find I'm getting better at following through algorithms and in taking a given task and turning it into code.

Would I recommend it to other people learning to code? Yes, but not to the exclusion of other types of learning. It skews towards the maths and computer science side of coding which is fine, but it perhaps takes you away from the 'engineering' thought process of organising and fitting together larger pieces of code into functioning products that solve a given problem or set of problems.

Come on, surely I can think of a simile than that to sound like I know what I'm talking about.

*"Think of it like taking swings in a batting cage as opposed to playing in a match"*

There. That'll have to do. Give it a go at [HackerRank](https://www.hackerrank.com)