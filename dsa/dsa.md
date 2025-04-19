# Data Structures & Algorithms

## Overview
DSA forms the foundation of efficient problem-solving in computer science.

## Data Structures

### Arrays
```python
arr = [1, 2, 3, 4, 5]
arr.append(6)      # O(1)
arr.pop()          # O(1)
arr[0]             # O(1) access
arr.insert(0, 0)   # O(n)
```

### Linked Lists
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None

# O(1) insertion at head
# O(n) search
```

### Stack (LIFO)
```python
stack = []
stack.append(1)    # push
stack.pop()        # pop
stack[-1]          # peek
```

### Queue (FIFO)
```python
from collections import deque
queue = deque()
queue.append(1)    # enqueue
queue.popleft()    # dequeue
```

### Hash Table
```python
d = {}
d['key'] = 'value'  # O(1) average
value = d.get('key') # O(1) lookup
```

### Trees
```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# BST: O(log n) search/insert (balanced)
```

### Heap
```python
import heapq
heap = []
heapq.heappush(heap, 3)  # O(log n)
heapq.heappop(heap)      # O(log n)
```

## Algorithms

### Sorting
- **Bubble Sort**: O(n²)
- **Merge Sort**: O(n log n)
- **Quick Sort**: O(n log n) average

### Searching
- **Linear Search**: O(n)
- **Binary Search**: O(log n)

### Binary Search
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

### DFS & BFS
```python
# DFS (Stack/Recursion)
def dfs(node):
    if not node: return
    print(node.val)
    dfs(node.left)
    dfs(node.right)

# BFS (Queue)
def bfs(root):
    queue = deque([root])
    while queue:
        node = queue.popleft()
        print(node.val)
        if node.left: queue.append(node.left)
        if node.right: queue.append(node.right)
```

## Big O Notation
- O(1): Constant
- O(log n): Logarithmic
- O(n): Linear
- O(n log n): Linearithmic
- O(n²): Quadratic
- O(2^n): Exponential

## Resources
- LeetCode
- Introduction to Algorithms (CLRS)
