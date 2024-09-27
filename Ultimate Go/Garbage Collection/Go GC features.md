- Non-generational;
- Non-compacting;
- Concurrent;
- Tricolor;
- Marked;
- Sweep collector.

**Non-compacting:** Memory on the heap is not moving, once an allocation is made on the heap its address is fixed for the lifetime of that allocation.

## Semantics
Default GC env variable is 100 which means when it should start the first collection, which evaluates to 4megs

The garbage collection runs in three different phases:
- **Mark start** - STW*;
- **Marking (Concurrent)** - Marking values that are in use and identifying those that are not;
-  **Mark termination** - STW*.

\* (Stop-The-World) phase, which means that there is no application work going on;

**Pro-tip:** Try to make sure that the STW phases are under 100 microseconds to reduce latency.

25% of the processing goes to the GC

Think of the heap as a graph of values (Tricolor mark and sweep):
- Starts at stacks;
- Steps:
	- Scan all the values and paint them white;
	- Scan the stacks looking for pointers out into the heap (root values) and paint them gray and put them to a queue;
	- Once the root value is out of the queue it'll be painted black and see if that new black values points to anything into the heap and if it does this value will be painted gray again and go back to the queue;
	- When everything is done all we got is white and black values;
- White values are values that are no longer in use and black values are values that are in use and we can't touch them;

*"If you want to be mechanically sympathetic you got two choices: we can reduce the number of allocations to speed the marking phase or we can reduce the amount of allocation which means that a GC doesn't take place until more work is done"* - William Kennedy