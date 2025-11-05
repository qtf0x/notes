---
tags:
  - Python
  - memory
  - references
---
You read that right; in Python, the default arraylist type, called `list`, is *not* implemented as a linked list, even though it can hold objects of different types. How? It uses a dynamic array to implement `list`, just like vectors in Rust or C++, but instead of an array of the list's objects, we get an array of pointers to heap-allocated objects.

This furthers Python's mission to be the slowest programming language around, for reasons you wouldn't even expect. To be fair, Common Lisp does [[Lisp cons cells hold pointers|something similar]].