---
tags:
  - references
  - lisp
---
[[Python lists are dynamic arrays of references|Like Python]], lists in Common Lisp hold pointers to objects rather than the objects themselves. That is, the `car` and `cdr` fields in each `cons` cell are both just pointers. This, of course, allows cells to 'hold' objects of any type.

An optimizing compiler like SBCL will probably store small, trivially copyable objects like small integers directly in the lower bits of `car` using **pointer tagging**.