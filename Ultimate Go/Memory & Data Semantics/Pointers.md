## Pass by Value (Value Semantics)

Value semantics means that every single function call is gonna operate on its own copy of the data, minimizing side effects and giving a high level of [[Integrity]]

The runtime will look for how many logical processors or cores the machine have

A goroutine is an application level thread which executes instructions sequentially leveraging the layer(OS level thread) that leverages the hardware.

 Every goroutine has its own memory stack and all of them fit in a 2k stack

The `&` operator before a variable refers to the address of said variable

- Value: What's in the box;
- Address: Where's the box;
- Data: Value and Address;

*"Any time a function is gonna operate in its own copy of the data we're gonna call this value semantics. This is the safest way to work with data in our programs."* - William Kennedy

Despite value semantics being safer it is not very efficient and it can add more complexity, an alternative to that is **pointer semantics** which share the value across the program boundaries making the program simpler but causing **side effects** that can also led to bugs

```go
count := 10
// This function will create a copy of count inside of it
increment(count)
```
## Sharing Data (Pointer Semantics)

Reduces code complexity and improve efficiency, but can cause side effects

The `*` operator before the type declaration refers to the value address instead of the value itself

```go
// This function will update the original count in main stack
func increment(inc *int){
	// Increment the "value of" that the "pointer points to"
	*inc++
}

func main(){
	count := 10

	// Pass the "address of" count
	increment(&count)
}
```

## Escape Analysis

"In Go we don't have constructors... But we do have what it called factory functions, functions that can construct a value, initialize it for properties and then return it back to the caller." - William Kennedy

"Stacks are self-cleaning." - William Kennedy

"Anything that's on the heap is the job for the garbage collector to manage" - William Kennedy

```go
package main

// user represents a user in the system
type user struct {
	name string
	email string
}

// main is the entry point for the application
func main() {
	u1 := createUserV1() // Value semantics
	u2 := createUserV2() // Pointer semantics

	println("u1", &u1, "u2", u2)
}


// createUserV1 creates a user value and passed a copy back to the caller
func createUserV1() user {
	u := user {
		name: "Bill",
		email: "bill@ardanlabs.com",
	}
	println("V1" &u)

	return u
}

// createUserV2 creates a user value and shares the value with the caller
func createUserV2() *user {
	u := user{
		name: "Bill",
		email: "bill@ardanlabs.com",
	}

	println("V2", &u)

	return &u // Escape on the heap
}
```

Go compiler can perform static code analysis and in the case of `createUserV2` the compiler performs a `Escape Analysis` which reads the code in compile time and try to determine where a value should be constructed in memory (in the stack or the heap), when the value is constructed on the `heap` we call that an `escape`. 

**Pro-tip:** Always use `value` when constructing a variable, and use the `pointer semantics` only in the return statement to improve [[Readability]].

```bash
go build -gcflags -m=2
```
Use this command to produce a `escape analysis` report.

## Stack Growth

"Allocation means when a value is constructed on the heap." - William Kennedy

**Contiguous Stack:** The function call that can't finish because there is not enough room on the stack will then double the size of the stack in a contiguous new frame of allocation.

"No goroutine can share a value with another goroutine that's on the stack." - William Kennedy



## Garbage Collection

"All collectors really have the same job. Their job is walk trough the heap identifying values that are currently allocated that are no longer needed or in use, and then sweep that memory free so that memory can be used again later on." - William Kennedy

**Pacer:** 
- Figure out when to start a collection, 
- How long that collection is going to take, 
- Make sure that it starts the collection at the very last moment yet it can still finish in time before we run out of heap space.

The GC will create an equal size gap of memory that will represent the total size of the heap.

"Internal latencies come with the garbage collector, that's a big part of it." - William Kennedy

The Garbage Collector will make use of at least one thread thus, creating latency.

The advantage of the GC is to help us to focus on the multi threading capabilities of Go without worrying about memory allocation.

**Pro-tip:** Try to minimize the number of requests it's taking to fill up the gaps and reducing the number of values on the heap.