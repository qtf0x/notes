---
tags:
  - c-plus-plus
  - strings
  - memory
  - references
---
In a language like C++, we often use an owned string type, i.e., `std::string`. The expected behavior is that this class will allocated its character buffer on the heap, and store a pointer to this memory along with a length and capacity:
```c++
struct string {
	char* data;
	size_t len;
	size_t cap;
};
```

We also expect that all three of these are one **machine word** wide (i.e., 64 bits on most modern machines).

However, to avoid needless heap allocations, and to make accessing and copying small strings more efficient, we can decide to use these three words as a buffer to store the string itself, directly in the string object. Implementations vary, but the idea is something like this:
```c++
struct string {
	union {
		struct big_str {
			char* data;
			size_t cap;
		};
		char small_str[sizeof(big_str)];
	};
	size_t len;
};
```

## How small is "small"?
It seems that, usually, there will be 1 bit for a small/big flag, 7 bits for the size of a small string, and one byte to NUL-terminate the string. Thus, we get **3 words minus 2 bytes**.

That's 10 chars on a 32-bit machine, or 22 chars on a 64-bit machine.

## References
https://stackoverflow.com/a/10319672
https://stackoverflow.com/a/21710033 ^383dc2