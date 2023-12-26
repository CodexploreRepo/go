# Variables

## Naming Convention

### File Naming

- Lowercase words separated with `_`
- File names begins with `.` or `_` are ignored by the go tool
- Test files in Go come with suffix `_test.go`. These are only compiled and run by the `go test` tool.
- Files with os and architecture specific suffixes automatically follow those same constraints
  - e.g. `name_linux.go` will only build on Linux, `name_amd64.go` will only build on AMD64.

### Function & Variable Naming

- **Convention**: use Camel case and should starts with a letter or underscore `_`. Eg. `userAge`
  - Constant should use all capital letters and use underscore `_` to separate words. Eg. `INT_MAX`
  - If variable type is `bool`, its name should start with `Has`, `Is`, `Can` or `Allow`, etc.
- **Exported names**: in Go, a name is exported if it begins with a capital letter.
  - Any "unexported" names are not accessible from outside the package.
  - For example, `Pi`, which is exported from the `math` package. Any "unexported" names are not accessible from outside the package.

```go
package main

import (
    "fmt"
    "math"
)

func main() {
    fmt.Println(math.Pi) // returns 3.141592653589793
    fmt.Println(math.pi) // error: undefined: math.pi

}
```

## Type

- **Type**: determine what kind of value you can store in the variable (**strongly-type**)

```go
var dir, file string // can declare multiple variables with the same type

var _speed int       // underscore
```

### Variables with initializers

- If an initializer is present, the type can be omitted; the variable will take the type of the initializer.

```go
var i, j int = 1, 2 // variables with initializers
var c, python, java = true, false, "no!"

```

### Type Conversion

- Syntax: `type(value)`

## Declaration

### Short-variable declearion

- _Inside a function_, the `:=` short assignment statement can be used in place of a `var` declaration with implicit type.
- _Outside a function_, every statement begins with a keyword (var, func, and so on) and so the `:=` construct is **not available**.

```go
func main() {
	var i, j int = 1, 2
	k := 3 // short declaration, only avail inside function
	c, python, java := true, false, "no!" // short declaration, only avail inside function

	fmt.Println(i, j, k, c, python, java)
}

```
