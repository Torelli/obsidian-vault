*"Integrity is about becoming very serious about reliability"* - William Kennedy
*"I call Go a data oriented designed language"* - William Kennedy

There are two driving forces behind integrity:

- Integrity is about memory allocation, read and write of memory being accurate, consistent and efficient. The type system is critical to making sure we have `micro` level of integrity
- Integrity is about every data transformation being accurate, consistent and efficient. Writing less code and error handling is critical to making sure we have this `macro` level of integrity
## **Write less code:**
There have been studies that have researched the numbers of bugs you can expect to have in your software. The industry average is around 15 to 50 bugs per 1000 lines of code. One simple way to reduce the number of bugs, and increase the integrity of your software, it to write less code.

48 critical failures have found in a study at a couple of hundred bugs in Cassandra, Hbase, HDFS, MapReduce, and Redis.

- 92%: Failures from bad error handling
	- 35%: Incorrect handling
		- 25%: Simply ignoring an error
		- 8%: Catching the wrong exception
		- 2%: Incomplete TODOs

*"Failure is expected, failure is not an odd case. Design systems that help you identify failure. Design systems that can recover from failure."* - JBD

*"Product excellence is the difference between something that only works under certain conditions, and something that only breaks under certain conditions"* - Kelsey Hightower