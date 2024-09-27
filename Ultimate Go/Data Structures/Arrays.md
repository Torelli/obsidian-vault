## Mechanical Sympathy

Cache system is used to get data closer to the hardware threads and reduce latency

*"The hardware has a prefetcher and the prefetcher's job is to look at your data access patterns and try to figure out what data is needed before its requested."* - William Kennedy

Cache uses a granularity of 64 byte (64 byte cacheline)

**Pro-tip:** Allocate a contiguous block of memory (arrays) and walk down that memory in a predictable stride to enable prefetching

**Be mechanical sympathetic!!**

**Pro-tip:** Get data into the processor efficiently instead of expect better hardware

## Semantics

- Optimize for correctness and understand the cost of the code ([[Correctness vs. Performance#^bd6920]]);
- *"There is efficiency in sharing but we have to worry about side effects"* - William Kennedy (See [[Pointers]])
- *"Lot of Go developers, even more experienced Go developers, they don't realize is that there's two flavors of the `for range` but each flavor actually represents a different **data semantics**."*  - William Kennedy
```go
// Value semantics
for i, fruit := range fruits {
	fmt.Println(i, fruit)	
}
// Pointer semantics
for i := range fruits {
	fmt.Println(i)
}
```

**General guideline:** When we're working with the built-in types (numeric, string or bool) use **value semantics** to move that data around the program (possible exception is to represent null in a struct).

## Range mechanics

```go
import "fmt"

func main() {
	// Using the pointer semantic form of the for range.
	friends := [5]string{"Annie", "Betty", "Charley", "Doug", "Edward"}
	fmt.Printf("Bfr[%s] : ", friends[1])

	for i := range friends {
		friends[1] = "Jack"

		if i == 1 {
			fmt.Printf("Aft[%s]\n", friends[1])
		}
	}
	fmt.Print("\n\n\n\n\n\n\n\n\n\n\n")
	// Output: Bfr[Betty] : Aft[Jack]

	// Using the value semantc form of the for range.
	friends = [5]string{"Annie", "Betty", "Charley", "Doug", "Edward"}
	fmt.Printf("Bfr[%s] : ", friends[1])

	for i, v := range friends {
		friends[1] = "Jack"

		if i == 1 {
			fmt.Printf("v[%s]\n", v)
		}
	}
	fmt.Print("\n\n\n\n\n\n\n\n\n\n\n")
	// Output: Bfr[Betty] : v[Betty]
}
```

\*The for in the value semantic will iterate over a copy of the array instead of the original one

