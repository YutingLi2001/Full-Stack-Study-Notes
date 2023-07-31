# Tuple

## Slicing
- Slice `A[1:4]` will start at index 1 and go up to, ==but not include, index 4.==
	-  Indices in Python are zero-based. So if we have the tuple `A = (1,2,3,4,5)`, then `A[1:4]` will give us the elements at indices 1, 2, and 3.

# List

## Append
- Append only adds one element to the list

## Sorted
- Returns a new list, will not change the original list

# Set

## Intersection Operation
- `&` : find the elements that are in both sets
	- `{'a','b'} & {'a'}`
	- The result is `{'a'}`

# Range Function

- `for x in range(0,3):`
- Will not reach upper bound, in this case 3
- think of `for(int i = 0; i < 3; i++)`

# Data Type
```python
import numpy as np
a=np.array([0,1,2,3,4])

# Check the type of the array
type(a)

# Check the type of the values stored in numpy arra
a.dtype
```

# Division
- Float division `1/2`
	- returns 0.5
- Integer division  `1//2`
	- returns 0