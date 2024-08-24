---
title: "Test Automation Is Not Magic"
date: 2022-12-23T19:20:13Z
draft: false
icon: 🪄
---

Over the years as I've been a part of numerous web development projects which lack test automation. A recurring theme is the idea that test automation is magic. It isn't. <!--more-->"Test automation will allow us to check hundreds of items in seconds", goes the thinking. "Once we create a test suite I can always just press a button to be assured of quality", it continues.

This is a dangerous and risky set of assumptions to make.

Test automation can help achieve your goals of course, but numerous other challenges and requirements are often forgotten in the pursuit of this imaginary happy land of automated quality. Here are some considerations.


### Is The Application Usefully Testable With Automation?

This is the most critical question to ask yourself and one that I've seen trip up many well meaning attempts to benefit from automated tests. Think carefully about the application you want to test. 

If it is unpredictable - for example it is hosted on a slow or unreliable test environment, or relies on numerous third parties - automation may produce numerous intermittent failures that are hard to address. 

If the application is under constant change, especially from work streams you may not have visibility of (third party integrations are often a cause here), failures may quickly swamp any created automation in required maintenance time and overwhelm its usefulness.

If the site has not been built to support automation, expect slow progress and a need to add data-test attributes to create reliable and effective tests - this might require developer or additional tester time investment.


### Does Your Team Know How To Do It?

You need people who can write reliable automation within a reasonable period of time. Respect this as you would any other technical skill, and don't assume it can be picked up effectively in a short period.

A common plan is to train existing manual testers with automated tools. It's tempting as a cost saving measure, and with the right people and enough support this can absolutely work. However it's a lengthy process and requires setting aside time from every day testing duties. The alternative is to hire new staff with automation skills which can take time and be costly.


### Have You Understood The Setup Process?

Approaching the automation of an existing project carries with it the requirement of a major investment up front.

You will spend a large amount of time in the project set up and creation of the initial set of tests.

* Framework and language
* Test report creation, storage and access
* Pipeline configuration and triggering
* Target test environment(s)
* Test data creation and usage

Even once these decisions are made, you will need to build up the test coverage itself over time before you begin to see serious benefits.


### Can You Maintain Your Tests?

Test automation is rarely just a one and done process. Unless the project is extraordinarily static, you can't write it then walk away dusting your hands.

On any reasonably sized and regularly updated code base your automation will need regular adjustment and care in order to keep it relevant and useful. New or changed behaviours, bug fixes and structural changes cause tests to need updating. The people tasked with this will need to have knowledge of the framework being used, the software under test and the automated test project itself.

This process goes chronically overlooked in almost every web project I've been a part of, and is especially difficult to handle when your automated tests are being carried out against partially completed work which might change several times a day. When and where to carry out updates is a fine balance to strike.


### How Will You Respond To Failures?

Once you've ensured your team has the skills, agreed on a set up, built your automation and have allocated time for maintenance, you're *still* not there. There's no point in tests if the failures are ignored.

Every time your tests run, if a failure is reported you need to be sure somebody will respond to it. Often the interpretation of such failures requires the same three items needed for effective maintenance - knowledge of the test framework, of the site you're testing and the test project.

The person responding needs to assess each failure and either update or fix the affected test, or raise an issue to be fixed.


### Conclusion

In conclusion, it is vital that you think about all these things *before* you decide that automation is the right solution for you. Automation is not magic and it will not instantly solve your problems. It will help you cover an immense number of checks in a short period but only if you invest time, effort and money into its creation as you would any other software project.

Are you genuinely confident in the following?

* The target website is reliable enough, reasonably set up to allow automation and not moving so fast as to make tests fragile and maintenance unmanageable.

* Your existing team has good knowledge of automation, they can be given the time and support to train in its use, or you can afford to hire additional specialist automation staff.

* You and your team fully understand all the decisions that go into creating a successful and useful set of automated tests.

* You are able to commit to having the capacity of people with knowledge of the site under test, the automation framework and the automation project available with enough capacity to handle maintenance and failure responses.