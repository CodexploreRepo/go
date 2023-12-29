# Structs, Arrays, Slices, and Maps

## Structs

- A `struct` is a collection of fields.
- Struct fields are accessed using a dot (`.`).
- Struct fields can be accessed through a struct `pointer`.
  - To access the field `X` of a struct when we have the struct pointer p we could write `(*p).X`. However, that notation is cumbersome, so the language permits us instead to write just `p.X`, without the explicit dereference.

```go
type Vertex struct {
	X int
	Y int
}

func main() {
    v:=Vertex{1,2}
	fmt.Println(v)     // {1,2}

    // access struct field via "."
    v.X = 4
    fmt.Println(v)     // {4,2}


    p:= &v             // struct pointer
    p.X = 1e9          // instead of (*p).X = 1e9
    fmt.Println(v)     // {1000000000 2}
}
```

## Arrays

- The type `[n]T` is an array of `n` values of type `T`.
  - An array's length is part of its type, so arrays cannot be resized.
- For example: `var a [10]int` declares a variable `a` as an array of 10 integers.

```go
func main() {
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1]) // Hello World
	fmt.Println(a)          // [Hello World]

	primes := [6]int{2, 3, 5, 7, 11, 13} // declare an array with initial values
	fmt.Println(primes)     //  [2 3 5 7 11 13]

  // let the compiler count the element for you
  b := [...]string{"Penn", "Teller"} // in this case, will be [2]string

}
```

## Slices

- An array has a fixed size.
- A `slice`, on the other hand, is a **dynamically-sized**, flexible view into the elements of an array. &#8594; The slice type is an abstraction built on top of Go’s array type
- A type `[]T` is a slice with elements of type T
- [Reading: Slices Intro](https://go.dev/blog/slices-intro)

```go
primes := [6]int{2, 3, 5, 7, 11, 13}

var s []int = primes[1:4] // "s" is a slice of "primes" array [3, 5, 7]
```

- A slice does not store any data, it just describes a section of an underlying array.
  - Changing the elements of a slice modifies the corresponding elements of its underlying array.

```go
// Changing the elements of a slice modifies the corresponding elements of its underlying array.
s[0] = 17
fmt.Println(s, primes)    // s=[17 5 7]; primes=[2 17 5 7 11 13]
```

### Slice Literals

- **Slice literals**: is like an array literal without the length.
  - For example: `[]bool{true, true, false}` this same as `[3]bool{true, true, false}`, then builds a slice that references it

```go
q := []int{2, 3, 5, 7, 11, 13}
fmt.Println(q)  // [2 3 5 7 11 13]

r := []bool{true, false, true, true, false, true}
fmt.Println(r)  // [true false true true false true]

s := []struct {
  i int
  b bool
}{
  {2, true},
  {3, false},
  {5, true},
  {7, true},
  {11, false},
  {13, true},
}
fmt.Println(s)  // [{2 true} {3 false} {5 true} {7 true} {11 false} {13 true}]
```

### Create a slice with `make`

- The make function allocates a zeroed array and returns a slice that refers to that array
  - To specify a capacity, pass a third argument to `make`:

```go
a := make([]int, 5)     // a=[0 0 0 0 0], len(a)=5, cap(a)=5
b := make([]int, 1, 5)  // b=[0]        , len(b)=1, cap(b)=5
```

### Slice length and capacity

- A **slice** is a descriptor of an array segment. It consists of

  - **Pointer** to the array.
  - **Length**
  - **Capacity**
  <p align="center"><img src="../../assets/img/slice.png" width=300></p>

- The **length** of a slice is the number of elements it contains.
- The **capacity** of a slice is the number of elements in the underlying array, _counting from the first element in the slice_.
  - The length and capacity of a slice `s` can be obtained using the expressions `len(s)` and `cap(s)`.

```go
// When the capacity argument is omitted, it defaults to the specified length.
s := make([]byte, 5, 5) //  s=[0,0,0,0,0]
len(s) == 5 // True
cap(s) == 5 // True
```

<p align="center"><img src="../../assets/img/slice-1.png" width=300></p>

- Now, let slice s by `s=s[2:4]`, observe the changes in the slice `s`, where the pointer now is moved to the third position in the underlying array, the length is 2, and capacity reduces to 3 only as counting from the first element in the slice which is from the third position

```go
s = s[2:4]  // s = [0,0]
len(s) == 2 // True
cap(s) == 3 // True
```

<p align="center"><img src="../../assets/img/slice-2.png" width=300></p>

- We can grow s to its capacity by slicing it again

```go
s = s[:cap(s)] // s = [0,0,0]
```

<p align="center"><img src="../../assets/img/slice-3.png" width=300></p>

- A slice cannot be grown beyond its capacity. Attempting to do so will cause a runtime panic

### Slices of slices

- Slices can contain any type, including other slices.

```go
// Create a tic-tac-toe board.
board := [][]string{
  []string{"_", "_", "_"},
  []string{"_", "_", "_"},
  []string{"_", "_", "_"},
}

// The players take turns.
board[0][0] = "X"
board[2][2] = "O"
board[1][2] = "X"
board[1][0] = "O"
board[0][2] = "X"
```

### Appending to Slice

- It is common to append new elements to a slice, and so Go provides a built-in `append` function.
- If the underlying array of `s` is too small to fit all the given values a bigger array will be allocated. The returned slice will point to the **newly allocated array**.

```go
var s []int
s = append(s, 1)        // [1]
s = append(s, 2, 3, 4)  // [1,2,3,4]
```

- To append one slice to another, use `...` to expand the second argument to a list of arguments.

```go
a := []string{"John", "Paul"}
b := []string{"George", "Ringo", "Pete"}
a = append(a, b...) // equivalent to "append(a, b[0], b[1], b[2])"
```
