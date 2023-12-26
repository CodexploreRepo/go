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
  - Constant should use all capital letters for the first letters. Eg. `MaxInt`
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

### Basic Types

- Go's basic types are

```go
bool // true & false

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128

// for example
import "math/cmplx"

var (
	ToBe   bool       = false                  // boolean
	MaxInt uint64     = 1<<64 - 1              // integer: 18446744073709551615
	z      complex128 = cmplx.Sqrt(-5 + 12i)   // complex: (2+3i)
)
```

#### Zero values

- Variables declared without an explicit initial value are given their zero value.

```go
func main() {
	var i int       // 0
	var f float64   // 0
	var b bool      // false
	var s string    // ""
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}


```

### Variables with initializers

- If an initializer is present, the type can be omitted; the variable will take the type of the initializer.

```go
var i, j int = 1, 2 // variables with initializers
var c, python, java = true, false, "no!"

```

### Type Conversion

- Syntax: `type(value)`

```go
var i int = 42
var f float64 = float64(i)  // convert i (integer) into float64
var u uint = uint(f)        // convert f (float64) into unsign integer
```

## Variable Declaration

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

## Constant

- Constants are declared like variables, but with the `const` keyword.
- Constants CANNOT be declared using the `:=` syntax.

```go
const World = "世界"
const Truth = true
```
