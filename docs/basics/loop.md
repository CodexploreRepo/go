# Loop

## For

- Go has only one looping construct, the `for` loop.
  - **Note**: Unlike other languages like C, Java, or JavaScript there are _no parentheses surrounding the three components of the `for` statement_
- The init and post statements are optional.

```go
package main

import "fmt"

func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum) // 45

    // The init and post statements are optional.
    sum := 1
	for ; sum < 1000; {
		sum += sum
	}
    // Hence: can convert to while loop
    for sum < 1000 {
		sum += sum
	}
    fmt.Println(sum) // 1024
}
```

## Range

- When `range` over the slice, it will return first is the index, and the second is a copy of the element at that index.

```go
var pow = [4]int{1, 2, 4}

func main() {
	for i, v := range pow {
		fmt.Printf("Index[%d] = %d\n", i,v)
	}
}

// Index[0] = 1
// Index[1] = 2
// Index[2] = 4
// Index[3] = 0
```

- You can skip the index or value by assigning to `_`.

```go
for i, _ := range pow
for _, value := range pow

// If you only want the index, you can omit the second variable.

for i := range pow
```
