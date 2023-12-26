# Pointers

## Introduction

- A pointer holds the memory address of a value.
- Pointer declaration: `*type` is a pointer to a value with `type`

```go
var p *int // p is a pointer to an integer
```

- `&` operator generates a pointer to its operand

```go
i := 42
p = &i // p point to i
```

- `*` operator denotes the pointer's underlying value. (also known as "dereferencing" or "indirecting")

```go
fmt.Println(*p) // read i through the pointer p, which is 42
*p = 21         // set i through the pointer p, i.e: i=21
fmt.Println(i)  // returns i=21
```
