---
tags:
  - Python
  - programming
  - inspection
---
We can use `locals()` or `globals()` to get a dictionary mapping all identifiers (as strings) to values, from the local or global scope, respectively.

```python
def foo(a, b, c):
	print(locals())

foo(1, 2, 3)
# {'a': 1, 'b': 2, 'c': 3}
```

If we need more precise information, for example types or info from a specific stack frame, we can also use the [[#^d40666|inspect]] module.

## References
https://docs.python.org/3/library/inspect.html ^d40666