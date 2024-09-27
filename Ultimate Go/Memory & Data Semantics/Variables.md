*"Type is life"* - William Kennedy

Type represents two things:
- The amount of the memory we are reading and writing;
- What that memory represents.

Without these two things there is no [[Integrity]]

A basic unity of memory in Go is a byte (which represents 8 bits), and a type can tell us what these bytes represents

There are three classes of types in Go:
- The built-in types;
- The reference types;
- User defined [[Struct Types]].

Everything you're doing is integer-based reading or writing, so it's important to use the most efficient precision for our integers, which the compiler can do for us.

Zero-value means that memory once allocated **has** to be initialized.

**Pro-tip:** Use the keyword *var* to denote a zero-value construction to improve [[Readability]] and consistency

A **word** is a generic allocation and it can represent either an integer or an address, in the case of strings (two words string value), the first word will be a pointer in which the zero-value will be *nil* and the second word will be an integer that represents the number of bytes for the string, in the case of a zero-value will be zero.

**Conversion over casting:**
Conversion allocate all the bytes needed, thus being safer than casting