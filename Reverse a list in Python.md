---
tags:
  - programming
  - Python
---
To get a new list, you can do:
```python
items = [1, 2, 3, 4, 5]

smeti = list(reversed(items)) # reversed returns an iterator
# OR
smeti = items[::-1] # slice backwards
```

To reverse the list in place:
```python
items.reverse()
```