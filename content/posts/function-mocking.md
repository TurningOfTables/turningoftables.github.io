---
title: "Extremely Basic Function Mocking"
date: 2024-03-29T09:43:12Z
draft: false
icon: 😆
---

A little exploration of small scale function mocking for Go testing<!--more-->

Function mocking is an area I hadn't really dipped into very much until recently. My main mocking experience has been verbal and network based, using tools like [Charles](https://www.charlesproxy.com/), [Mountebank](http://www.mbtest.org/) and the like.

The concept is similar of course, except instead of mocking network responses or requests you're mocking functions.

What took a little bit of thinking through was where the mocks actually need to 'be'. Like network mocks (mostly), you don't really want to call your mocks directly from the tests, because that doesn't prove anything. You set up mocks and then call the function under test. The function under test then makes onward calls which is where the mocks get hit.

Here it is represented badly with arrows: `Test <-> function under test <-> mocked function calls`

Your test then asserts that it gets the expected result and, as a bonus with many mocking libraries available, you can assert that the expected function calls were carried out to your mocks.

Where this comes together really nicely in Go is with interfaces. Because interfaces in Go are implicitly satisfied when a type implements all the methods defined by an interface, it's easy to 'slide in' your mock functions instead of the real thing during test setup.

Let's say you have the following very contrived example:

```
// main.go
package main

import "time"

type TimeHelper interface {
	Get() string
}

type Time struct{}

func (l *Time) Get() string {
	t := time.Now().String()
	return t
}
```

Pretty simple. A type of Time with a method of Get() that returns the current time. This satisfies the interface TimeHelper.

You have the below code which creates an instance of Time and calls your function 'getMeTheTime':

```
// time.go
package main

import (
	"fmt"
)

func main() {
	res := GetMeTheTime(&Time{})
	fmt.Println(res)
}

func GetMeTheTime(sh TimeHelper) string {
	return sh.Get()
}
```

If you create a regular test, you'll always get back a different result depending on what time it is, which is a pain to test for. Instead, we can create a mock type which satisfies the TimeHelper interface, but with a Get method that always returns whatever you give it

```
// time_mock.go
package main

type MockTime struct{}

// Always returns what is provided as a string
func (ml *MockTime) Get(input string) string {
	return input
}

```

Then in our test, we can write the following:

```
// main_test.go

package main

import (
	"testing"
)

func TestGetMeTheTime(t *testing.T) {
	mock := MockTime{}
	expected := "2000-01-01 01:01:01.000000001 +0000 UTC"

	res := GetMeTheTime(&mock)

	if res != expected {
		t.Errorf("expected: %v, got: %v", expected, res)
	}
}
```

So my terrible diagram with more specific names could now look like this:

```
TestGetMeTheTime <-> 
GetMeTheTime(passing a mock that implements the expected interface param) <-> 
MockTime's version of Get() is called, which always returns a static time that we can test for
```

This is an extremely bare bones implementation as I experiment with the idea and make it go into my brain, but hopefully it gets the pattern across reasonably well. 

Creating mocks at a larger scale would likely benefit from the use of a library for generating reliable mock methods and allow asserting that method calls were actually made. It's beyond the scope of this post but very popular are several libraries which will generate sets of mock methods for a given interface. Two I've come across so far are [mockery](https://github.com/vektra/mockery) and Uber's [mock](https://github.com/uber-go/mock) which is a fork of the original [mock](https://github.com/golang/mock), now archived.