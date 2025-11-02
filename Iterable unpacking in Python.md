---
tags:
  - Python
  - programming
---
Python has some neat syntax sugar for destructuring. We can unpack sequences
**explicitly**:
```python
def foo(x, y, z):
	return x + y + z

bar = (1, 2, 3)
foo(*bar) # equivalent to foo(1, 2, 3)

# Also works with dictionaries using the ** operator
baz = {'x': 1, 'y': 2}
qux = {**baz, 'z': 3, 'w': 4}

# The above is equivalent to the more verbose:
# qux = baz.copy()
# qux.update({'z': 3, 'w': 4})
```

Or, we can unpack sequences **implicitly** in variable assignments. The
*starred* expressions get a list containing the values not assigned to the
other, *mandatory* expressions.
```python
seq = [1, 2, 3, 4]
first, *rest, last = seq
# first = 1, rest = [2, 3], last = 4

# Note that this doesn't work (there are no mandatory exprs):
*every = seq
# But this does:
*every, = seq
```

We don't need this syntax (it's sugar, remember?), but it's a little nicer than the alternatives:
```python
# For a list:
seq = [1, 2, 3, 4]
first, rest, last = seq[0], list(seq[1:-1]), seq[-1]

# For an iterable:
it = iter(seq)
first, rest = it.next(), list(it)
```

## References
https://peps.python.org/pep-0448/
https://peps.python.org/pep-3132/