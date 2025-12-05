# Python Cheat Sheet

A Cheat Sheet 📜 to **revise** Python syntax in **less time**. Particularly useful for solving Data Structure and Algorithmic problems or a quick overview before an interview.

> [Click here for similar Java Resource (not made by me)](https://drive.google.com/file/d/1ao4ZA28zzBttDkuS6MLQI52gDs_CJZEm/view) <br>
> Get a PDF of this sheet at the end. <br>
> Leave a ⭐ if you like the cheat sheet (contributions welcome!) <br>

# Table of Contents
- [Basics](#basics)
- [Data Structures](#data-structures)
  - [Lists](#lists)
  - [Dictionary](#dictionary)
  - [Counter](#counter)
  - [Deque](#deque)
  - [Heapq](#heapq)
  - [Sets](#sets)
  - [Tuples](#tuples)
  - [Strings](#strings)
- [Built-in Functions](#built-in-functions)
- [Useful Modules](#useful-modules)
  - [Random](#random)
- [Advanced Topics](#advanced-topics)
- [Best Practices](#best-practices)
- [Tips & Gotchas](#tips--gotchas)

# Basics

## Data Types
![Python Data Types](https://user-images.githubusercontent.com/59110866/173563442-1a6fa3d2-b569-4eb0-99cc-9b91cc8be1eb.png)

## Operator Precedence
![Python Operators](https://user-images.githubusercontent.com/47276307/172329850-61fc0809-a4b0-416c-848b-1c502ecb4772.jpg)

# Data Structures

## Lists
Time Complexities:
![List Operations](https://user-images.githubusercontent.com/47276307/172330098-1c5f0a6e-7f80-4f4f-9be6-1d734e2c70cd.jpg)

```python
nums = [1,2,3]

# Common Operations
nums.index(1)      # Find index
# Example: [1,2,3].index(1) → 0

nums.append(1)     # Add to end
# Example: [1,2,3].append(1) → [1,2,3,1]

nums.insert(0,10)  # Add 10 from left (at index 0 which is start)
# Example: [1,2,3].insert(0,10) → [10,1,2,3]

nums.remove(3)     # Remove value
# Example: [1,2,3].remove(3) → [1,2]

nums.pop()         # Remove & return last element
# Example: [1,2,3].pop() → 3, nums becomes [1,2]

nums.sort()        # In-place sort (TimSort: O(n log n))
# Example: [3,1,2].sort() → [1,2,3]

nums.reverse()     # In-place reverse
# Example: [1,2,3].reverse() → [3,2,1]

nums.copy()        # Return shallow copy
# Example: [1,2,3].copy() → [1,2,3] (new list)

# List Slicing
nums[start:stop:step]  # Generic slice syntax
# Example: [1,2,3,4,5][1:4:2] → [2,4]

nums[-1]    # Last item
# Example: [1,2,3][-1] → 3

nums[::-1]  # Reverse list
# Example: [1,2,3][::-1] → [3,2,1]

nums[1:]    # Everything after index 1
# Example: [1,2,3,4][1:] → [2,3,4]

nums[:3]    # First three elements
# Example: [1,2,3,4,5][:3] → [1,2,3]

# Check if element is in list
if element in nums:
    print("Element is in list")
else:
    print("Element is not in list")
```

## Dictionary
Time Complexities:
![Dictionary Operations](https://user-images.githubusercontent.com/47276307/172330107-e68e3228-1c76-4bfb-bb38-04d18f94d5b9.jpg)

```python
d = {'a':1, 'b':2}

# Essential Operations
d['key'] = value         # Add/update key-value pair
# Example: d['c'] = 3 → {'a':1, 'b':2, 'c':3}

d.get('key', default)     # Safe access with default
# Example: d.get('a', 0) → 1, d.get('x', 0) → 0

d.setdefault('key', 0)    # Set if missing
# Example: d.setdefault('c', 0) → 0, d becomes {'a':1, 'b':2, 'c':0}

d.items()                 # Key-value pairs
# Example: d.items() → dict_items([('a', 1), ('b', 2)])

d.keys()                  # Just keys
# Example: d.keys() → dict_keys(['a', 'b'])

d.values()               # Just values
# Example: d.values() → dict_values([1, 2])

d.pop(key)              # Remove and return value
# Example: d.pop('a') → 1, d becomes {'b':2}

d.update({key: value})  # Batch update
# Example: d.update({'c':3, 'd':4}) → {'a':1, 'b':2, 'c':3, 'd':4}


# Advanced Usage
from collections import defaultdict
d = defaultdict(list)     # Auto-initialize missing keys
d = defaultdict(list)       # Auto-initialize missing keys as empty lists
d['key'].append(1)          # No need to check if key exists
d['key'].append(2)
# Result: {'key': [1, 2, 3]}

d = defaultdict(int)      # Useful for counting
```

## Counter
```python
from collections import Counter

# Initialize
c = Counter(['a','a','b'])    # From iterable
# Example: Counter(['a','a','b']) → Counter({'a': 2, 'b': 1})

c = Counter("hello")          # From string
# Example: Counter("hello") → Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})

# Operations
c.most_common(2)      # Top 2 frequent elements
# Example: Counter('hello').most_common(2) → [('l', 2), ('h', 1)]

c['a'] += 1           # Increment count
# Example: c['a'] += 1 → c['a'] becomes 3

c.update("more")      # Add counts from iterable
# Example: Counter('hi').update('hi') → Counter({'h': 2, 'i': 2})

c.total()             # Sum of all counts
# Example: Counter({'a': 2, 'b': 1}).total() → 3
```

## Deque
Time Complexities:
![Deque Operations](https://user-images.githubusercontent.com/47276307/172330115-78500420-3276-4e45-8ce3-fd668b7eb14e.jpg)

```python
from collections import deque

# Perfect for BFS - O(1) operations on both ends
d = deque()
# Example: d = deque() → deque([])

d.append(1)          # Add right
# Example: deque([2]).append(1) → deque([2, 1])

d.appendleft(2)      # Add left
# Example: deque([1]).appendleft(2) → deque([2, 1])

d.pop()              # Remove right
# Example: deque([2,1]).pop() → 1, d becomes deque([2])

d.popleft()          # Remove left
# Example: deque([2,1]).popleft() → 2, d becomes deque([1])

d.extend([1,2,3])    # Extend right
# Example: deque([1]).extend([2,3]) → deque([1, 2, 3])

d.extendleft([1,2,3])# Extend left
# Example: deque([4]).extendleft([1,2,3]) → deque([3, 2, 1, 4])

d.rotate(n)          # Rotate n steps right (negative for left)
# Example: deque([1,2,3]).rotate(1) → deque([3, 1, 2])
```

## Heapq

```python
import heapq

# MinHeap Operations - All O(log n) except heapify
nums = [3,1,4,1,5]
heapq.heapify(nums)          # Convert to heap in-place: O(n)
# Example: heapq.heapify([3,1,4]) → [1, 3, 4]

heapq.heappush(nums, 2)      # Add element: O(log n)
# Example: heapq.heappush([1,3,4], 2) → [1, 2, 4, 3]

smallest = heapq.heappop(nums)  # Remove smallest: O(log n)
# Example: heapq.heappop([1,2,3]) → 1, heap becomes [2, 3]

# MaxHeap Trick: Multiply by -1
nums = [-x for x in nums]    # Convert to maxheap: O(n)
# Example: [-x for x in [1,2,3]] → [-1, -2, -3]

heapq.heapify(nums)          # O(n)
# Example: heapq.heapify([-3,-1,-2]) → [-3, -1, -2]

largest = -heapq.heappop(nums)  # Get largest: O(log n)
# Example: -heapq.heappop([-3,-1,-2]) → 3

# Advanced Operations
k_largest = heapq.nlargest(k, nums)    # O(n * log k)
# Example: heapq.nlargest(2, [3,1,4,2]) → [4, 3]

k_smallest = heapq.nsmallest(k, nums)  # O(n * log k)
# Example: heapq.nsmallest(2, [3,1,4,2]) → [1, 2]

# Custom Priority Queue
heap = []
heapq.heappush(heap, (priority, item))  # Sort by priority
# Example: heapq.heappush([], (2, 'b')) → [(2, 'b')]
```

## Sets
Time Complexities:
![Untitled](https://user-images.githubusercontent.com/47276307/172330132-7a785f5f-bbc6-43b9-b82f-794190813787.jpg)

```python
s = {1,2,3}

# Common Operations
s.add(4)             # Add element
# Example: {1,2,3}.add(4) → {1, 2, 3, 4}

s.remove(4)          # Remove (raises error if missing)
# Example: {1,2,3,4}.remove(4) → {1, 2, 3}

s.discard(4)         # Remove (no error if missing)
# Example: {1,2,3}.discard(4) → {1, 2, 3} (no error)

s.pop()              # Remove and return arbitrary element
# Example: {1,2,3}.pop() → 1 (arbitrary), set becomes {2, 3}

# Set Operations
a.union(b)           # Elements in a OR b
# Example: {1,2}.union({2,3}) → {1, 2, 3}

a.intersection(b)    # Elements in a AND b
# Example: {1,2}.intersection({2,3}) → {2}

a.difference(b)      # Elements in a but NOT in b
# Example: {1,2}.difference({2,3}) → {1}

a.symmetric_difference(b)  # Elements in a OR b but NOT both
# Example: {1,2}.symmetric_difference({2,3}) → {1, 3}

a.issubset(b)        # True if all elements of a are in b
# Example: {1,2}.issubset({1,2,3}) → True

a.issuperset(b)      # True if all elements of b are in a
# Example: {1,2,3}.issuperset({1,2}) → True
```

## Tuples
```python
# Tuples are immutable lists
t = (1, 2, 3, 1)

# Essential Operations
t.count(1)      # Count occurrences of value
# Example: (1, 2, 3, 1).count(1) → 2

t.index(2)      # Find first index of value
# Example: (1, 2, 3, 1).index(2) → 1

# Useful Patterns
x, y = (1, 2)   # Tuple unpacking
# Example: x, y = (1, 2) → x=1, y=2

coords = [(1,2), (3,4)]  # Tuple in collections
# Example: List of coordinate tuples
```

## Strings
```python
s = "hello world"

# Essential Methods
s.split()            # Split on whitespace
# Example: "hello world".split() → ['hello', 'world']

s.split(',')         # Split on comma
# Example: "a,b,c".split(',') → ['a', 'b', 'c']

s.strip()            # Remove leading/trailing whitespace
# Example: "  hello  ".strip() → 'hello'

s.lower()            # Convert to lowercase
# Example: "Hello".lower() → 'hello'

s.upper()            # Convert to uppercase
# Example: "hello".upper() → 'HELLO'

s.isalnum()          # Check if alphanumeric
# Example: "abc123".isalnum() → True

s.isalpha()          # Check if alphabetic
# Example: "abc".isalpha() → True, "abc123".isalpha() → False

s.isdigit()          # Check if all digits
# Example: "123".isdigit() → True, "12a".isdigit() → False

s.find('sub')        # Index of substring (-1 if not found)
# Example: "hello".find('ll') → 2, "hello".find('x') → -1

s.count('sub')       # Count occurrences
# Example: "hello".count('l') → 2

s.replace('old', 'new')  # Replace all occurrences
# Example: "hello world".replace('l', 'L') → 'heLLo worLd'

# ASCII Conversion
ord('a')             # Char to ASCII (97)
# Example: ord('a') → 97

chr(97)              # ASCII to char ('a')
# Example: chr(97) → 'a'

# Join Lists
''.join(['a','b'])   # Concatenate list elements
# Example: ''.join(['a','b','c']) → 'abc'
```

# Built-in Functions

```python
# Iteration Helpers
enumerate(lst)        # Index + value pairs
# Example: list(enumerate(['a','b'])) → [(0, 'a'), (1, 'b')]

zip(lst1, lst2)      # Parallel iteration
# Example: list(zip([1,2], ['a','b'])) → [(1, 'a'), (2, 'b')]

map(fn, lst)         # Apply function to all elements
# Example: list(map(str, [1,2,3])) → ['1', '2', '3']

filter(fn, lst)      # Keep elements where fn returns True
# Example: list(filter(lambda x: x>1, [1,2,3])) → [2, 3]

any(lst)             # True if any element is True
# Example: any([False, True, False]) → True

all(lst)             # True if all elements are True
# Example: all([True, True, False]) → False

del lst[idx] # Delete idx element. Can be used for dictionary(e.g., del dic[key])
# Example: lst = [1,2,3]; del lst[0] → [2, 3]

# Binary Search (import bisect)
bisect.bisect(lst, x)     # Find insertion point
# Example: bisect.bisect([1,2,4,5], 3) → 2

bisect.bisect_left(lst, x)# Find leftmost insertion point
# Example: bisect.bisect_left([1,2,2,3], 2) → 1

bisect.insort(lst, x)     # Insert maintaining sort
# Example: lst=[1,3]; bisect.insort(lst, 2) → [1,2,3]

# Type Conversion
int('42')            # String to int
# Example: int('42') → 42

str(42)              # Int to string
# Example: str(42) → '42'

list('abc')          # String to list
# Example: list('abc') → ['a', 'b', 'c']

''.join(['a','b'])   # List to string
# Example: ''.join(['a','b','c']) → 'abc'

set([1,2,2])         # List to set
# Example: set([1,2,2,3]) → {1, 2, 3}

# Math
abs(-5)              # Absolute value
# Example: abs(-5) → 5

pow(2, 3)            # Power
# Example: pow(2, 3) → 8

round(3.14159, 2)    # Round to decimals
# Example: round(3.14159, 2) → 3.14
```

# Useful Modules

## Random
```python
import random

# Selection
random.choice([1, 2, 3, 4])      # Random element from sequence
# Example: random.choice([1, 2, 3, 4]) → 3 (random)

random.choices([1, 2, 3], k=2)   # k random elements (with replacement)
# Example: random.choices([1, 2, 3], k=2) → [2, 2] (may have duplicates)

random.sample([1, 2, 3], k=2)    # k unique random elements (without replacement)
# Example: random.sample([1, 2, 3], k=2) → [3, 1] (no duplicates)

# Random Numbers
random.randint(1, 10)             # Random integer in [1, 10] (inclusive)
# Example: random.randint(1, 10) → 7 (random, includes 10)

random.randrange(1, 10)          # Random integer in [1, 10) (exclusive end)
# Example: random.randrange(1, 10) → 5 (random, excludes 10)

random.random()                   # Random float in [0.0, 1.0)
# Example: random.random() → 0.8234 (random)

random.uniform(1.0, 10.0)        # Random float in [1.0, 10.0]
# Example: random.uniform(1.0, 10.0) → 5.67 (random)

# Shuffling
nums = [1, 2, 3, 4]
random.shuffle(nums)             # Shuffle list in-place
# Example: random.shuffle([1,2,3,4]) → [3,1,4,2] (shuffled)
```

# Advanced Topics

## Custom Sorting with cmp_to_key
```python
from functools import cmp_to_key

def compare(item1, item2):
    # Return -1: item1 comes first
    # Return 1:  item2 comes first
    # Return 0:  items are equal
    if item1 < item2:
        return -1
    elif item1 > item2:
        return 1
    return 0

# Sort using custom comparison
sorted_list = sorted(items, key=cmp_to_key(compare))

# Default sorted() behavior
sorted([3, 1, 2])              # [1, 2, 3] - Ascending (default)
sorted([3, 1, 2], reverse=True) # [3, 2, 1] - Descending
```

## Taking Multiple Inputs
```python
# Basic multiple input
x, y = input("Enter two values: ").split()

# Multiple integers
x, y = map(int, input("Enter two numbers: ").split())

# List of integers
nums = list(map(int, input("Enter numbers: ").split()))

# Multiple inputs with custom separator
values = input("Enter comma-separated values: ").split(',')

# List comprehension method
x, y = [int(x) for x in input("Enter two numbers: ").split()]
```

## Math Module Essentials
```python
import math

# Constants
math.pi       # 3.141592653589793
# Example: math.pi → 3.141592653589793

math.e        # 2.718281828459045
# Example: math.e → 2.718281828459045

# Common Functions
math.ceil(2.3)        # 3 - Smallest integer greater than x
# Example: math.ceil(2.3) → 3, math.ceil(-2.3) → -2

math.floor(2.3)       # 2 - Largest integer less than x
# Example: math.floor(2.3) → 2, math.floor(-2.3) → -3

math.gcd(a, b)        # Greatest common divisor
# Example: math.gcd(48, 18) → 6

math.log(x, base)     # Logarithm with specified base
# Example: math.log(8, 2) → 3.0

math.sqrt(x)          # Square root
# Example: math.sqrt(16) → 4.0

math.pow(x, y)        # x^y (prefer x ** y for integers)
# Example: math.pow(2, 3) → 8.0

# Trigonometry
math.degrees(rad)     # Convert radians to degrees
# Example: math.degrees(math.pi) → 180.0

math.radians(deg)     # Convert degrees to radians
# Example: math.radians(180) → 3.141592653589793
```

## Important Python Integer Operations
```python
# Binary representation
bin(10)              # '0b1010'
format(10, 'b')      # '1010' (without prefix)

# Division and Modulo
divmod(10, 3)        # (3, 1) - returns (quotient, remainder)

# Negative number handling
x = -3
y = 2
print(x // y)        # -2 (floor division)
print(int(x/y))      # -1 (preferred for negative numbers)
print(x % y)         # 1 (Python's modulo with negative numbers)
```

# Best Practices

## Documentation
```python
def binary_search(arr, target):
    """
    Find target in sorted array using binary search.
    Args:
        arr: Sorted list of numbers
        target: Number to find
    Returns:
        Index of target or -1 if not found
    """
    pass
```

## Testing
```python
# Use assertions for edge cases
assert binary_search([], 1) == -1, "Empty array should return -1"
assert binary_search([1], 1) == 0, "Single element array should work"
```

# Tips & Gotchas

1. Integer Division:
```python
# Use int() for consistent negative number handling
print(-3//2)        # Returns -2
print(int(-3/2))    # Returns -1 (usually desired)
```

2. Default Dictionaries:
```python
# Prefer defaultdict for frequency counting
from collections import defaultdict
freq = defaultdict(int)
for x in lst:
    freq[x] += 1    # No KeyError if x is new
```

3. Heap Priority:
```python
# For custom priority in heapq, use tuples
heap = []
heapq.heappush(heap, (priority, item))
```

4. List Comprehension:
```python
# Often clearer than map/filter
squares = [x*x for x in range(10) if x % 2 == 0]
```

5. String Building:
```python
# Use join() instead of += for strings
chars = ['a', 'b', 'c']
word = ''.join(chars)  # More efficient
```

6. Using Sets for Efficiency:
```python
# O(1) lookup for contains operations
seen = set()
if x in seen:  # Much faster than list lookup
    print("Found!")
```

7. Custom Sort Keys:
```python
# Sort by length then alphabetically
words.sort(key=lambda x: (len(x), x))
```

8. Default Arguments Warning:
```python
# Don't use mutable defaults
def bad(lst=[]):     # This can cause bugs
    lst.append(1)
    return lst

def good(lst=None):  # Do this instead
    if lst is None:
        lst = []
    lst.append(1)
    return lst
```

---
Made with ❤️ for fellow leetcoders.
