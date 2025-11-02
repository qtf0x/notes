---
tags:
  - computer-architecture
  - assembly
  - x86
  - bit-twiddling
---
**Logical shift**: Bits are moved left or right and new bits are *filled with zeros*.
**Arithmetic shift**: The same as a logical shift, except that new bits introduced on the left by a right shift are *filled to match the most-significant bit*.

In most programming languages, a right shift causes an arithmetic shift, as this
effectively performs *sign extension*. The result of a right shift is thus
equivalent to dividing by a power of two, except that the result is *rounded
toward $-\infty$*, not toward zero as we would typically do in mathematics.

That is, **a right arithmetic shift is equivalent to flooring a division by a power of two**, not a regular division!
$$x \gg n \equiv \left\lfloor \frac{x}{2^n} \right\rfloor$$

The above is the difference between these instructions:
```x86
SAL/SAR # arithmetic shifts
SHL/SHR # logical shifts
IDIV    # signed divide (rounds toward 0)
```

## References
https://en.wikipedia.org/wiki/Arithmetic_shift
https://en.wikipedia.org/wiki/Floor_and_ceiling_functions
https://dl.acm.org/doi/10.1145/956641.956647