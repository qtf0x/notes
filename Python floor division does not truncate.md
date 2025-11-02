---
tags:
  - Python
  - programming
  - mathematics
  - division
---
The `//` operator in Python **does not truncate** as I used to believe. It **floors** the result, which is not the same!
```python
7 // 3
# 2 (an integer, rounded down from 2.333)
-7 // 3
# -3 (an integer, rounded down from -2.333)
```

The truncation function is equivalent to ceiling for numbers less than zero and to floor for numbers greater than zero:
$$
\operatorname{trunc}\left( x \right)
\begin{cases} 
	\left\lfloor x \right\rfloor & x \geq 0 \\
	\left\lceil x \right\rceil & x < 0
\end{cases}
$$
In mathematics, this function is a little different (see the Wikipedia page below).

## References
https://www.boot.dev/lessons/2ab1d6b9-3f00-414c-a4b5-3d95ab104bd0
https://en.wikipedia.org/wiki/Truncation