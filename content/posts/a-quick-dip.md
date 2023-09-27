---
title: "A Quick Dip Into Svelte"
date: 2023-09-27T12:18:56Z
draft: false
icon: 🏊
---

I've been meaning to try making something using Svelte about fourteen times now <!--more-->, but never quite had any inspiration on exactly what to make. Thankfully
a friend of mine helped out; he wanted a way to track the holiday he booked from work, and found the provided tool hard to use.

After around 4 total days of work time, I had an application using Svelte, SvelteKit and TailwindCSS with the following features:

* Registration, with user password bcrypt encrypted
* Login/logout
* Set and display used and total amount of annual allowance
* Add, display and delete holidays
* Add, display and delete excluded holiday periods
* Historical holidays are marked to indicate they have already been taken
* Calculate days used as business days, ignoring weekends
* Validation prevents overlapping holidays or excluded holiday periods, holidays which end before they start etc.
* Data storage in SQLite DB
* Basic browser tests with Playwright
* Unit tests for date utils using Vitest

### How Was It?

Initially it was a little bit strange having to confirm to quite an opinionated structure for the project in SvelteKit. Using the `+page` file naming took a while to get used to, but as I progressed and was adding more features
into the structure already created, it started to become quite natural. I don't know if this is strictly the best way to think about it, but mentally `+page.svelte` became a view to me, and `+page.server.js` effectively became a controller.

Structurally, common actions like adding a new button to interact with my SQLite data store, displaying data back into the user's page, applying my own logic or conversions to that data, even adding authentication were relatively simple within SvelteKit. I was able to put the code
in a place that felt right, and pass data between different concerns with confidence. 

Svelte itself does a good job of allowing you not to worry too much about keeping the DOM up to date, and inserting basic logic into what to display. I found passing props around and understanding what data was available where to be much simpler than with React, and the lifecycles of a component were less of a worry, as was state management. Some of the syntax feels a little bit strange (`$: yourVariable` for example), but the tutorial explains it well and it quickly becomes second nature. Despite bouncing off React a few times, I found
I was able to get into Svelte more easily, produce what I wanted, and not fight the tech but work with it.

Overall it was a good experience, and when I look at the features that I was able to implement in less than a full work week it's clear that it was a very productive set of tools to work with.

### Would you do it again?

Maybe! I have to say that my main reservation was not to do with Svelte, SvelteKit or TailwindCSS. It was that I missed writing code in Go. JavaScript felt a little bit vague and uncertain by comparison, and I missed having a simple and clear
set of tools to solve problems with. That being said I did appreciate the JS ecosystem when working with things like dates (using `date-fns`), which made some quite fiddly checks for different date-related things much easier.

To be honest I've missed Go though so I'm going back to that next. I've been linked a good looking framework called beego that definitely seems worth a look


### References / Further Reading

- [Svelte](https://svelte.dev/)
- [SvelteKit](https://kit.svelte.dev/)
- [TailwindCSS](https://tailwindcss.com/)
- [beego](https://github.com/beego/beego)