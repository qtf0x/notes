---
tags:
  - Python
  - programming
  - scripting
---
As an interpreted scripting language, Python doesn’t have the equivalent of a standard entrypoint function, often called `main()` in compiled languages. The Python interpreter simply executes statements in order.

Many Python programmers will mimic the behavior of a program in their scripts by writing a function called `main()` near the top of the file, which calls functions declared throughout the rest of the file to get some process started. There is *no issue with the order of definitions*, as a single call to `main()` will then be placed at the bottom of the file.

```python
def main():
    # uses the definitions below

# function and class definitions

main()
```