# Functions

## Introduction

- An example of a Go's function:
  - `add` takes two parameters of type `int`.
  - returns the value as type `int` as well

```go
func add(x int, y int) int {
	return x + y
}

// shorten way of declearing input parameters
func add(x, y int) int {
	return x + y
}
```

- A function can return **multiple results**.

```go
func swap(x, y string) (string, string) {
	return y, x
}
```

- Named return values: A `return` statement **without arguments** returns the named return values. This is known as a **"naked" return**.
  - Naked return statements should be used only in **short** functions. They can harm readability in longer functions.

```go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17)) // return x=7 & y=10
}
```

## `fmt.Print` functions

- `fmt.Printf`: format string
  - `%T` is to get the type of the variable
  - `%v` is to get the value of the variable
  - `%g` is to format the float values

```go
import (
	"fmt"
)

var (
	ToBe   bool       = false
	MaxInt uint64     = 1<<64 - 1
)

func main() {
	fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)      // Type: bool Value: false
	fmt.Printf("Type: %T Value: %v\n", MaxInt, MaxInt)  // Type: uint64 Value: 18446744073709551615
}

```
