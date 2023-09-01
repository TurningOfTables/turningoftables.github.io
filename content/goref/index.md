---
title: "Go Quick Reference"
date: 2023-01-21T12:18:56Z
draft: false
type: "goref"
kind: "single"
---

A quick set of memory prompts for common patterns in Go. To avoid repetition they usually don't contain the surrounding code to make them runnable (like `package main` or `import`)

- [For Loops](#for-loops)
  - [Basic](#basic)
  - [With Index, Value](#with-index-value)
- [Error Handling](#error-handling)
  - [Basic](#basic-1)
  - [Using Short Statement If](#using-short-statement-if)
- [JSON Handling](#json-handling)
  - [Struct -\> JSON](#struct---json)
  - [JSON -\> Struct](#json---struct)
- [Functions](#functions)
  - [Anonymous](#anonymous)
  - [Assigning to a variable](#assigning-to-a-variable)
  - [Variadic](#variadic)
  - [Deferred call](#deferred-call)
- [Testing](#testing)
  - [Basic](#basic-2)
  - [With testify assertions](#with-testify-assertions)
  - [Benchmark function](#benchmark-function)
  - [Example function](#example-function)
- [Fiber](#fiber)
  - [Passing Variable to Handler](#passing-variable-to-handler)
  - [Testing](#testing-1)
    - [HTTP GET Response](#http-get-response)
    - [HTTP POST Response](#http-post-response)


## For Loops
___

### Basic

```
var numbers = []int{1, 2, 3}

for i = 0, i <= len(numbers), i ++ {
	fmt.Printf("value: %d\n", numbers[i])
}
```



### With Index, Value

```
var numbers = []int{1, 2, 3}

for index, value := range numbers {
	fmt.Printf("index: %d, value: %d\n", index, value")
}
```



## Error Handling
___


### Basic


```
data, err := io.Readfile(filename)
if err != nil {
	panic(err)
}
```


### Using Short Statement If

```
if err := json.Unmarshal(a, &b); err != nil {
	panic(err)
}
```

## JSON Handling
___

### Struct -> JSON

```
type Movie struct {
	Title string
	Year int
}

movie := Movie{Title: "Bee Movie", Year: 2007}

output, err := json.Marshal(movie)
if err != nil {
	panic (err)
}

fmt.Println(output) // byte array
```

### JSON -> Struct

```
type Movie struct {
	Title string
	Year int
}

var movie Movie
resp, err := http.Get("https://www.example.com")
if err != nil {
	panic(err)
}

b, err := io.ReadAll(resp.Body)
if err != nil {
	panic(err)
}
defer resp.Body.Close()

if err := json.Unmarshal(b, &movie); err != nil {
	panic(err)
}
```

## Functions
___

### Anonymous

```
func main() {
	func(){
		fmt.Println("I am an anonymous function")
	}()
}
```

### Assigning to a variable

```
func main() {
	afunc := func(){
		fmt.Println("I am an anonymous function")
	}
	
	afunc()
}
```

### Variadic

```
func sum(vals ...int) int {
	total := 0
	for _, val := range vals {
		total += val
	}
	
	return total
}
```

### Deferred call

```
func netRequest(url string) error {
	resp, err := http.Get(url)
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()
}
```

## Testing
___

### Basic
```
func TestSum(t *testing.T) {
	res := Sum(1, 2)
	if res != 3 {
		t.Errorf("Sum(1, 2) = %d; want 3", res)
	}
}
```


### With testify assertions

```
func TestSum(t *testing.T) {
	res := Sum(1, 2)
	assert.Equal(t, 3, res)
}
```

### Benchmark function

```
func BenchmarkSum(b *testing.B) {
	for i := 0; i < b.N; i ++ {
		Sum(1, 2)
	}
}
```

### Example function

```
func ExampleSum() {
	res := Sum(1, 2)
	fmt.Println(res)
	// Output: 3
}
```

## Fiber

### Passing Variable to Handler

```
somevar := "foo"
app.Get("/", func(c *fiber.Ctx) error {
    return indexHandler(c, somevar)
})
```


### Testing

Assumes you have abstracted setup for your app into an initApp(), such that this returns an instance of the app with configuration such as routes already in place.

#### HTTP GET Response


```
func TestGet(t *testing.T) {
    app := initApp() 

    req := httptest.NewRequest(http.MethodGet, "/", nil)
    resp, err := app.Test(req)
    if err != nil {
        t.Error(err)
    }

    assert.Equal(t, 200, resp.StatusCode)
}

```

#### HTTP POST Response
```
func TestPost(t *testing.T) {

    postBody := 
    app := initApp()

    req := httptest.NewRequest(http.MethodPost, "/", )
}
```