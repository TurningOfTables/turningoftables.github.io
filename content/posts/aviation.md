---
title: "In Aviation"
date: 2023-01-21T12:18:56Z
draft: false
icon: 🪁
---

An important lesson that has been learned in safety critical environments such as aviation over decades of flying and - sadly - numerous accidents, is that one layer of safety is not enough.<!--more-->

In aviation, important actions are always checked and confirmed multiple times, often by different people using different methods or with different areas of expertise.

When an air traffic controller gives an instruction, the pilot reads back critical parts of it to confirm it has been received and understood correctly. When an important setting is changed in the cockpit, the pilot monitoring will cross-check and often read back the change to confirm it is as expected.

This idea extends backwards through all the hardware and software on a plane, with extensive testing and redundancy adding further layers before the pilot may even encounter it during a flight.

Layers upon layers add up and the result is an incredibly safe form of transport where only the most bizarre and convoluted series of events can result in anything approaching a fatal incident. Sometimes this is referred to as the Swiss Cheese Model.


### How We Can Apply Its Lessons

In an everyday software environment we can use some of the same ideas.

Traditionally you might have a developer write code and pass the resulting software over to a tester who is then responsible for finding all the bugs before release.

Unfortunately that leaves us with just one layer, and so it only takes a single failure to result in defects going unnoticed. Instead, think how you can build up your own system of layers to make it ever more difficult for issues to pass through the process unchecked.

#### People

By building a culture where quality is the responsibility of everybody in the process, you add in layers of people with different specialisms and different perspectives who are always looking for potential pitfalls. From your product owner, through your designs, as part of the engineering and of course when testers become involved - if everybody is thinking quality then the opportunities to spot problems increase dramatically. Product owners can help test and verify they are getting what they expect, designers can create robust designs which account for unexpected user behaviour, developers can carry out careful code reviews and - perhaps most importantly - run their own code to check it works before considering it ready for testing.

Every single person involved needs a quality mindset, not just your test team.

#### Tools

Then, you add tooling to give you even more layers! Developers can make good use of unit tests, functional tests and static code analysis. When part of the build pipeline these can stop many potential issues before the software is even deployed for testing.

Testers can supplement their role with effective and reliable automated functional, system or integration checks, and production monitoring and testing tools can help to find or prevent issues encountered at deployment.

Adding these tools acts as a 'force multiplier', enabling you to cover a lot of ground on simple checks very quickly and freeing your testers to focus on more complex, creative or exploratory testing.

### Conclusion

Layers. Build up as many layers of both people and technology working to improve quality within your team as you can.

By doing this you make it harder and harder for unknown defects to reach production, the software development process is smoother and more predictable. Most importantly - quality increases.


### References / Further Reading

- [Wikipedia - Swiss Cheese Model](https://en.wikipedia.org/wiki/Swiss_cheese_model)
- [Admiral Cloudberg - Amazing articles on aviation accidents and safety](https://admiralcloudberg.medium.com/)