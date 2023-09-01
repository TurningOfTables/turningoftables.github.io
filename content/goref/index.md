---
title: "Go Quick Reference"
date: 2023-01-21T12:18:56Z
draft: false
type: "goref"
kind: "single"
---

## For Loops
___

### Basic For Loop

```
var numbers = []int{1, 2, 3}

for i = 0, i <= len(numbers), i ++ {
	fmt.Printf("value: %d\n", numbers[i])
}
```



### For Loop With Index, Value

```
var numbers = []int{1, 2, 3}

for index, value := range numbers {
	fmt.Printf("index: %d, value: %d\n", i, v")
}
```



## Error Handling
___


### Basic Error Handling


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

### Marshall struct into JSON

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

### Unmarshall JSON into struct

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

### Anonymous function

```
func main() {
	func(){
		fmt.Println("I am an anonymous function")
	}()
}
```

### Assigning an anonymous function to a variable

```
func main() {
	afunc := func(){
		fmt.Println("I am an anonymous function")
	}
	
	afunc()
}
```

### Variadic function

```
func sum(vals ...int) int {
	total := 0
	for _, val := range vals {
		total += val
	}
	
	return total
}
```

### Deferred function call

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

### Basic test function
```
func TestSum(t *testing.T) {
	res := Sum(1, 2)
	if res != 3 {
		t.Errorf("Sum(1, 2) = %d; want 3", res)
	}
}
```


### Basic test function (with testify)

```
func TestSum(t *testing.T) {
	res := Sum(1, 2)
	assert.Equal(t, 3, res)
}
```

### Basic benchmark function

```
func BenchmarkSum(b *testing.B) {
	for i := 0; i < b.N; i ++ {
		Sum(1, 2)
	}
}
```

### Basic example function

```
func ExampleSum() {
	res := Sum(1, 2)
	fmt.Println(res)
	// Output: 3
}
```