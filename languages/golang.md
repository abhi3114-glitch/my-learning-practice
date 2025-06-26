# Go (Golang)

## Overview
Go is a statically typed, compiled language designed at Google. It provides simplicity, high performance, and excellent support for concurrent programming through goroutines and channels.

## Core Concepts

### Basic Syntax
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

### Variables and Data Types
```go
// Variable declaration
var name string = "John"
var age int = 30
var isActive bool = true

// Short declaration
name := "John"
count := 42

// Constants
const Pi = 3.14159
const (
    StatusOK = 200
    StatusNotFound = 404
)

// Basic types
var (
    integer    int     = 42
    float      float64 = 3.14
    complex    complex128 = 1 + 2i
    str        string  = "hello"
    boolean    bool    = true
    byteVal    byte    = 255
    runeVal    rune    = 'A'
)

// Zero values
var i int       // 0
var f float64   // 0.0
var b bool      // false
var s string    // ""
```

### Collections
```go
// Arrays (fixed size)
var arr [5]int = [5]int{1, 2, 3, 4, 5}
arr2 := [...]int{1, 2, 3}

// Slices (dynamic)
slice := []int{1, 2, 3, 4, 5}
slice = append(slice, 6)
subSlice := slice[1:4]

// Make slice with capacity
nums := make([]int, 5, 10)  // len=5, cap=10

// Maps
m := make(map[string]int)
m["key"] = 42
value, exists := m["key"]

m2 := map[string]int{
    "one": 1,
    "two": 2,
}
delete(m2, "one")
```

### Control Flow
```go
// If-else
if x > 0 {
    // positive
} else if x < 0 {
    // negative
} else {
    // zero
}

// If with init statement
if val, err := getValue(); err == nil {
    fmt.Println(val)
}

// Switch
switch day {
case "Monday", "Tuesday":
    fmt.Println("Early week")
case "Friday":
    fmt.Println("TGIF")
default:
    fmt.Println("Another day")
}

// Type switch
switch v := i.(type) {
case int:
    fmt.Println("Integer:", v)
case string:
    fmt.Println("String:", v)
}

// For loop (only loop in Go)
for i := 0; i < 10; i++ { }
for i < 10 { }  // while-like
for { }         // infinite
for i, v := range slice { }
for k, v := range m { }
```

### Functions
```go
// Basic function
func add(a, b int) int {
    return a + b
}

// Multiple return values
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

// Named return values
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return  // naked return
}

// Variadic functions
func sum(nums ...int) int {
    total := 0
    for _, n := range nums {
        total += n
    }
    return total
}

// Function as value
fn := func(x int) int { return x * 2 }

// Closures
func counter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

// Defer
func example() {
    defer fmt.Println("This runs last")
    fmt.Println("This runs first")
}
```

### Structs and Methods
```go
// Struct definition
type Person struct {
    Name string
    Age  int
}

// Creating structs
p1 := Person{Name: "John", Age: 30}
p2 := Person{"Jane", 25}
p3 := new(Person)  // Returns pointer

// Methods
func (p Person) Greet() string {
    return "Hello, " + p.Name
}

// Pointer receiver (can modify)
func (p *Person) Birthday() {
    p.Age++
}

// Embedding (composition)
type Employee struct {
    Person
    Department string
}

emp := Employee{
    Person:     Person{Name: "John", Age: 30},
    Department: "Engineering",
}
emp.Greet()  // Inherited method
```

### Interfaces
```go
// Interface definition
type Writer interface {
    Write([]byte) (int, error)
}

type Reader interface {
    Read([]byte) (int, error)
}

// Combining interfaces
type ReadWriter interface {
    Reader
    Writer
}

// Implementing interfaces (implicit)
type MyWriter struct{}

func (w MyWriter) Write(data []byte) (int, error) {
    fmt.Println(string(data))
    return len(data), nil
}

// Empty interface (any type)
func describe(i interface{}) {
    fmt.Printf("Type: %T, Value: %v\n", i, i)
}

// Type assertion
value, ok := i.(string)
if ok {
    fmt.Println("String:", value)
}
```

### Concurrency
```go
// Goroutines
go doWork()

go func() {
    fmt.Println("Anonymous goroutine")
}()

// Channels
ch := make(chan int)       // Unbuffered
ch := make(chan int, 10)   // Buffered

ch <- 42       // Send
value := <-ch  // Receive
close(ch)

// Select
select {
case msg := <-ch1:
    fmt.Println("Received:", msg)
case ch2 <- message:
    fmt.Println("Sent")
case <-time.After(time.Second):
    fmt.Println("Timeout")
default:
    fmt.Println("No communication")
}

// Worker pool pattern
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)
    
    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }
    
    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)
}

// Sync primitives
var mu sync.Mutex
mu.Lock()
defer mu.Unlock()

var wg sync.WaitGroup
wg.Add(1)
go func() {
    defer wg.Done()
    // work
}()
wg.Wait()
```

### Error Handling
```go
// Basic error handling
result, err := someFunction()
if err != nil {
    return fmt.Errorf("failed: %w", err)
}

// Custom errors
type CustomError struct {
    Code    int
    Message string
}

func (e *CustomError) Error() string {
    return fmt.Sprintf("%d: %s", e.Code, e.Message)
}

// Panic and recover
func mayPanic() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered:", r)
        }
    }()
    panic("something went wrong")
}
```

## Best Practices

1. **Handle errors explicitly** - don't ignore them
2. Use **gofmt** for consistent formatting
3. Keep **packages small and focused**
4. Use **interfaces** for abstraction
5. Prefer **composition** over inheritance
6. Use **context** for cancellation/timeouts
7. **Don't communicate by sharing memory; share memory by communicating**

## Common Packages
- net/http (HTTP server/client)
- encoding/json (JSON)
- database/sql (Database)
- context (Context handling)
- sync (Synchronization)
- testing (Unit tests)

## Resources
- Tour of Go
- Effective Go
- Go by Example
