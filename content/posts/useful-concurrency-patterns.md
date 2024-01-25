---
title: "A Useful Go Concurrency Pattern - WaitGroups and Buffered Channels"
date: 2024-01-25T15:33:27Z
draft: false
icon: 🔃
---

While improving my knowledge of how Go implements concurrency, and various ways of handling it, I came across some useful common patterns which I found helpful as a baseline to build in.

I split my requirements for concurrency into two parts:

* The ability to safely spin out work into multiple 'workers' that improves overall execution time.
* The ability to limit or throttle the number of workers that can be active at the same time.

The below example implements both of these, using two features of Go. WaitGroups, and buffered channels.

### WaitGroups

WaitGroups are designed to allow you to wait for more than one goroutine to complete before your program exits. Without a WaitGroup or equivalent functionality your program will exit before your goroutines have a chance to do their work. It essentially works by incrementing a counter for each goroutine, and decrementing it when it completes. Then you wait until the counter is 0 to know all goroutines are done.

To use them:

1. Create an instance of WaitGroup
2. Each time you spin up a goroutine, call `Add(1)` on your WaitGroup
3. Within your goroutine, call `Done()` when its work is complete. This is usually done with `defer` to ensure it executes
4. In your `main()` function, call `Wait()` to block until all workers are complete.


### Buffered Channels

Sometimes called a semaphore approach, this works by using a buffered channel set to the size of the maximum concurrent workers you want to allow. When a worker begins work, it 'takes' a slot by sending a value to the buffered channel. Once the worker is complete it 'gives back' the slot by receiving a value from the buffered channel.

If the buffered channel reaches its capacity as more workers take slots, it will block until the channel has capacity, effectively limiting the number of concurrent workers.

To use them:

1. Create a buffered channel that is the size of the maximum concurrency you want to allow. It's common to make it a channel that accepts type struct{}, e.g `c := make(chan struct{}, 5)` - in this case we want our max concurrency to be 5.
2. When a worker begins work, take up a slot by sending to the channel `c <- struct{}{}`
3. When a worker completes work, give back the slot by receiving from the channel `<- c`

### A Complete Example

The below example uses the [httpbin.org](https://httpbin.org/) service for API requests, and implements a random delay to make the jobs take a variable amount of time.

```
package main

import (
	"fmt"
	"math/rand"
	"net/http"
	"sync"
	"time"
)

var maxConcurrency = 2 // the most number of workers we want to allow
var jobs = 4 // how many jobs there are to be done

func main() {
	fmt.Printf("Starting %d jobs (max concurrent: %d)\n", jobs, maxConcurrency)
	startTime := time.Now()
	c := make(chan struct{}, maxConcurrency) // create our buffered channel so we can limit workers
	var wg sync.WaitGroup // create our WaitGroup instance

	for x := 1; x <= jobs; x++ {
		wg.Add(1) // register our worker
		go doWork(x, c, &wg) // start our worker
	}

	wg.Wait() // wait for number of registered workers to be 0
	fmt.Printf("All jobs complete in %v", time.Since(startTime))
}

func doWork(x int, c chan struct{}, wg *sync.WaitGroup) {
	defer wg.Done() // ensure that the WaitGroup counter is decremented when the function returns
	startTime := time.Now()
	c <- struct{}{} // Take a slot from the buffered channel
	queueTime := time.Since(startTime)

	artificialDelay := rand.Intn(3)
	url := fmt.Sprintf("https://httpbin.org/delay/%d", artificialDelay)
	http.Get(url)
	fmt.Printf("Completed job %d in %v  (queue time %v)\n", x, time.Since(startTime), queueTime)

	<-c // Give back the slot to the buffered channel
}

```

Running the above gives us output similar to the following

```
Starting 4 jobs (max concurrent: 2)
Completed job 1 in 404.0926ms  (queue time 0s)
Completed job 4 in 1.4033671s  (queue time 0s)
Completed job 2 in 1.5535537s  (queue time 406.1108ms)
Completed job 3 in 2.6434148s  (queue time 1.4061137s)
All jobs complete in 2.6518036s
```

As we can see, we have two jobs that started immediately (with no queue time), and two jobs that had to wait because our maximum concurrency was two.

### Further Reading/Inspiration


* [Redowan's Reflections: Limit goroutines with buffered channels](https://rednafi.com/go/limit_goroutines_with_buffered_channels/)
* [Go WaitGroup Documentation](https://pkg.go.dev/sync#WaitGroup)
* [Go Making Slices Maps and Channels](https://go.dev/ref/spec#Making_slices_maps_and_channels)


