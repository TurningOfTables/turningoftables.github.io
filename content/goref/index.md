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
  - [Single condition](#single-condition)
  - [Infinite loop](#infinite-loop)
  - [Ending loops](#ending-loops)
  - [With Index, Value](#with-index-value)
- [Commonly used format 'verbs' for printing](#commonly-used-format-verbs-for-printing)
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
- [SQL](#sql)
  - [Connect to DB](#connect-to-db)
  - [Query DB](#query-db)
  - [Query Row DB](#query-row-db)
  - [Exec DB](#exec-db)
- [Data Types](#data-types)
  - [Maps](#maps)
    - [Create](#create)
    - [Set key/value](#set-keyvalue)
    - [Clear key/value](#clear-keyvalue)
    - [Check for key presence](#check-for-key-presence)
  - [Slices](#slices)
    - [Create](#create-1)
    - [Create with length](#create-with-length)
    - [Set value](#set-value)
    - [Literal](#literal)
    - [Append](#append)
    - [Slice up to but not including element](#slice-up-to-but-not-including-element)
    - [Slice from and including element](#slice-from-and-including-element)
    - [Multi-dimensional](#multi-dimensional)
- [HTTP](#http)
  - [GET Request](#get-request)
  - [POST Request With Body](#post-request-with-body)
  - [With headers](#with-headers)
  - [With query params](#with-query-params)
  - [Parse JSON Response Body](#parse-json-response-body)
- [Type conversion](#type-conversion)
  - [string \<-\> T (int, float, bool)](#string---t-int-float-bool)
- [Generics](#generics)


## For Loops
___

### Basic

```
var numbers = []int{1, 2, 3}

for i = 0, i <= len(numbers), i ++ {
	fmt.Printf("value: %d\n", numbers[i])
}
```

### Single condition
```
i := 1
for i <= 3 {
    fmt.Println(i)
    i ++
}
```

### Infinite loop
```
for {
    fmt.Println("And again")
}
```

### Ending loops
```
break // breaks out of the entire loop
continue // starts the next iteration of the current loop
```


### With Index, Value

```
var numbers = []int{1, 2, 3}

for index, value := range numbers {
	fmt.Printf("index: %d, value: %d\n", index, value")
}
```



## Commonly used format 'verbs' for printing

```
    %v – default format
    %+v - default format with field names
    %d – base 10
    %g – float
    %t – boolean
    %s – string
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
___


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
type Movie struct {
    Title string
    Year int
}

func TestPost(t *testing.T) {

    postBody := Movie{Title: "Bee Movie", Year: 2007}
    json, err := json.Marshal(postBody)
    if err != nil {
        t.Error(err)
    }
    reader := bytes.NewReader(json)

    app := initApp()
    req := httptest.NewRequest(http.MethodPost, "/", )
    resp, err := app.Test(req)
    if err != nil {
        t.Error(err)
    }

    var m Movie
    defer resp.Body.Close()
    body, err := io.ReadAll(resp.Body)
    if err != nil {
        t.Error(err)
    }

    if err := json.Unmarshal(body, &m); err != nil {
        t.Error(err)
    }

    assert.Equal(t, 201, resp.StatusCode)
    assert.Equal(t, Movie{Title: "Bee Movie", Year: 2007}, m)

}
```

## SQL

___


### Connect to DB

```
db, err := sql.Open("postgres", "postgresql://user:password@localhost/database?sslmode=disable")
if err != nil {
    panic(err)
}
```

### Query DB

```
type Movie struct {
    Title string
    Year int
}

var movies []Movie


rows, err := db.Query("SELECT * FROM movies)
if err != nil {
    panic(err)
}
defer rows.Close()

for rows.Next() {
    var movie Movie
    if err := rows.Scan(&movie.Title, &movie.Year); err != nil {
        panic(err)
    }
    cars = append(cars, car)
}
```

### Query Row DB

```
type Movie struct {
    Title string
    Year int
}

var movie Movie
searchId := 1
row := db.QueryRow("SELECT * FROM movies WHERE id = $1", searchId)
row.Scan(&movie.Title, &movie.Year)

if movie.ID != searchId {
    panic("No entry found")
}
```

### Exec DB

```
type Movie struct {
    Title string
    Year int
}

m := Movie{Title: "Bee Movie", Year: 2007}

_, err := db.Exec("INSERT into movies (title, year) VALUES ($1, $2)", movie.Title, movie.Year)
if err != nil {
    panic(err)
}
```

## Data Types



### Maps

[Full docs](https://pkg.go.dev/maps)

#### Create
```
m := make(map[string]int)
```

#### Set key/value
```
m := make(map[string]int)
m["k1"] = 1
```

#### Clear key/value
```
m := map[string]int{"foo": 1}
delete(m, "foo")
```

#### Check for key presence
```
m := map[string]int{"foo": 1}

_, ok := m["bar"]
if !ok {
    fmt.Println("Not found")
} else {
    fmt.Println("Found")
}

// Not found
```

### Slices

[Full docs](https://pkg.go.dev/slices)

#### Create 
```
var s []string
```

#### Create with length
```
s := make([]string, 3)
```

#### Set value
```
s := make([]string, 3)
s[0] = "a"
```

#### Literal
```
t := []string{"a", "b", "c"}
```

#### Append
```
t := []string{"a", "b", "c"}
t = append(t, "d")
```

#### Slice up to but not including element
```
t := []string{"a", "b", "c"}
l := t[:2]
// [a b]
```

#### Slice from and including element
```
t := []string{"a", "b", "c"}
l := t[1:]
// [b c]
```

#### Multi-dimensional
```
multi := make([][]int, 3)
for i := 0; i < len(multi); i ++ {
    multi[i] = make([]int, 2)
    for j := 0; j < 2; j++ {
        multi[i][j] = 1
    }
}
// [[1 1] [1 1] [1 1]]
```

## HTTP

### GET Request

```
res, err := http.Get("https://www.example.com")
if err != nil {
    panic(err)
}

// Do something with the response
```

### POST Request With Body
```
someBody := "informationtosend"

res, err := http.Post("https://www.example.com", "text/plain", strings.NewReader(someBody))
if err !+ nil {
    panic(err)
}

// Do something with the response
```

### With headers
```
req, _ := http.NewRequest("GET", "https://www.example.com", nil)
req.Header.Set("X-Api-Key", "mykey")
res, err := http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}

// Do something with the response
```

### With query params
```
params := url.Values{
    "yourparam1": {"yourparamvalue1"},
    "yourparam2": {"yourparamvalue2"},
}

req, _ := http.NewRequest("GET", "https://www.example.com" + params.Encode(), nil)
res, err := http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}

// Do something with the response
```

### Parse JSON Response Body
```

type Res struct {
    Foo string
    Bar string
}

res, err := http.Get("https://www.example.com")
if err != nil {
    panic(err)
}

b, err := io.ReadAll(res.Body)
if err != nil {
    panic(err)
}

var r Res

// Reads b []byte into r Res
if err := json.Unmarshal(b, &r); err != nil {
    panic(err)
}


```

## Type conversion

### string <-> T (int, float, bool)

See [strconv package](https://pkg.go.dev/strconv#Atoi)

## Generics

```
// Create an interface with a union type to be your constraint

type Number interface {
    int64 | float64
}

// Create your function with a type parameter using your type constraint from above

function sumAllNumbers[K comparable V Number](m map[K]V) V {
    var s V
    for _, v := range v {
        s += v
    }
    return s
}

```

Note that you must be able to perform all actions on all allowed types for code to compile.