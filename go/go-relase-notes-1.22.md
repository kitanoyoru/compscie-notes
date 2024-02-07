# Core changes

### Changes in `for` loops

1. Previously, the variables declared by a "for" loop were created once and updated by each iteration. In Go 1.22, each iteration of the loop creates new variables, to avoid accidental sharing bugs. 

**Example**

```go
package main

import (
	"fmt"
	"sync"
)

const N = 5

func main() {
	wg := sync.WaitGroup{}

	wg.Add(N)

	for i := 0; i < N; i++ {
		func() {
			defer wg.Done()
			fmt.Printf("%v ", i)
		}()
	}
wg.Wait()
}

// Output: 0 1 2 3 4
```

2. "For" loops may now range over integers.

**Example**

```go
package main

import "fmt"

func main() {
  for i := range 10 {
    fmt.Println(10 - i)
  }
  fmt.Println("go1.22 has lift-off!")
}
```

### Runtime

The runtime now keeps type-based garbage collection metadata nearer to each heap object, improving the CPU performance (latency or throughput) of Go programs by **1–3%**. This change also reduces the memory overhead of the majority Go programs by approximately **1%** by deduplicating redundant metadata. Some programs may see a smaller improvement because this change adjusts the size class boundaries of the memory allocator, so some objects may be moved up a size class.
