# Structs, Slices, and Maps

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
