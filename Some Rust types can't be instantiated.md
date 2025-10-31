---
tags:
  - programming
  - Rust
  - types
---
In most typed languages, **values** have types and any value can be assigned to
a variable of the corresponding type. Thus, a variable can be of any type.
Rust's type system is a little different, in that *some types apply only to
values*, and cannot be used as the type of a variable. Indeed, what are called
[[dynamically-sized types]] (DSTs) cannot be instantiated at all, as their size
is unknown at compile time.

For example, in C, there exist the `char` and `char*` types, which represent a
one-byte ASCII character and the address of such a character, respectively. Both
of these describe values, and either can be used as the type of a variable
holding such a value. There is no notion of a "string" in C, other than a
`char*` pointer to the first character of one. Array types *sort of* have a
length associated with them, but decay to raw pointers as soon as we start
passing them around.

In Rust, on the other hand, we have the `str` type, which is a DST representing
the type of an actual string *value* - some collection of UTF-8 characters in
memory, of unknown size. Or at least the size isn't baked into the type. It
isn't a pointer to the start of the string; it represents the value of the
string itself. This is why we can't instantiate a variable of type `str`, as the
size of all variables must be known at compile time. Instead, if we want to
refer to a string in memory, we always borrow a slice (i.e., a `&str`), which
really is just a pointer and a length. In the same way, we cannot instantiate a
raw array type such as `[u8]`; all of our array variables are either
stack-allocated and have the size baked into the type (e.g., `[u8; 12]`), or are
slices into an array (e.g., `&[u8]`).