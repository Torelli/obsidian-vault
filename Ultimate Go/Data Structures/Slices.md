## Declare, Length & Reference Types

- Arrays might be the most important data structure as relates to the hardware but not the most important as relates to Go
- Slices are Go's most important data structure
- Slices are dynamic arrays
- Slice is part of class of type called reference type (There are 3 types: built-in, struct types and reference types)

Setting length when creating a slice:
```go
func main() {
	// Create a slice with a length of 5 elements.
	fruits := make([]string, 5)
	fruits[0] = "Apple"
	fruits[1] = "Orange"
	fruits[2] = "Banana"
	fruits[3] = "Grape"
	fruits[4] = "Plum"

	// You can't access an index of a slice beyong its length.
	fruits[5] = "Runtime error"

	// Error: panic: runtime error: index out of range
	fmt.Println(fruits)
}
```

*"Slice is always a three-word data structure"* - William Kennedy
1. Pointer to the backing array set to a zero-value;
2. Length;
3. Capacity;

**Pro-tip:** use value [[Pointers#Pass by Value (Value Semantics)]] for reference types to move the data around the program.

Even though value semantics are being used to move the data around, when we are reading and writing reference types we are using [[Pointers#Sharing Data (Pointer Semantics).]]

Setting both length and capacity when creating a slice:
```go
func main() {
	// Create a slice with a length of 5 elements and a capacity of 8.
	fruits := make([]string, 5, 8)
	fruits[0] = "Apple"
	fruits[1] = "Orange"
	fruits[2] = "Banana"
	fruits[3] = "Grape"
	fruits[4] = "Plum"

	inspectSlice(fruits)
}

// inspectSlice exposes the slice header for review
func inspectSlice(slice []string) {
	fmt.Printf("Length[%d] Capacity[%d]\n", len(slice), cap(slice))
	for i, s := range slice {
		fmt.Print("[%d] %p %s\n",
			i,
			&slice[i],
			s)
	}
}
```

*"Capacity really just represents efficiency for future growth"* - William Kennedy