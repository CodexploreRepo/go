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
