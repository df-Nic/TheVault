---
Title: Memoization
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - Algorithms/DynamicProgramming
---

The concept of memoization is to record all values that was previously computed.

A memoized function:
- A table which stores all previous calls
- Use inputs as keys to store or retrieve values

```Python
memoize_table = {}

def memoize(f, name):
	if name not in memoize_table:
		memoize_table[name] = {}
	table = memoize_table[name]

	def helper(*args*):
		if args in table:
			return memoize_table[args]
		else:
			result = f(*args*)
			memoize_table[args] = result
			return result

	return helper

def memo_fib(n):
	def helper(n):
		if n == 0:
			return 0
		elif n == 1:
			return 1
		else:
			return memo_fib(n-1) + memo_fib(n-2)

	return memoize(helper,"memo_fib")(n)
```

Once a value is computed, it is remembered in the table. Therefore, the next time the function is called with the same argument it just needs to retrieve the value from the table if it has been calculated.