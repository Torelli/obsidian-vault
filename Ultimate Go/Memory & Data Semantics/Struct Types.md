Your ability to define the data that you need

*"Implicit conversion of types is the Halloween special of coding. Whoever thought of them deserves their own special hell."* - Martin Thompson

Struct types are composite types, which mean that they are based on other existing types.

Alignments will push extra bytes to the struct (padding byte) to improve performance

Ordering the fields from largest to smallest will reduce padding and optimize performance

**Pro-tip:** Only worry about optimizing performance when its actually a problem ([[Correctness vs. Performance]])

We can create both named and unnamed types (Anonymous types)

```go
// Named type
type person struct {
	name string
	age int
}

// Declare a variable of an anonymous type set to its zero value.
var e1 struct {
	name string
	age int
}

// Declare a variable of an anonymous type and init using a struct literal.
e2 := struct {
	name string
	age int
} {
	name: "bill",
	age: 32
}
```

Two identical and/or compatible **named structs** will be treated as different types by the compiler (No implicit conversion)
