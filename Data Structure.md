---
title: Data Structure
created: '2021-07-09T05:45:35.274Z'
modified: '2021-07-09T08:20:01.736Z'
---

# Data Structure

## Heap

### Building a heap from an array

Given an array that represents a complete binary tree(CBT), we can heapify elements in O(N) instead of O(NlogN) by taking into consideration that the leaf nodes doesn't need to be heapified. 

```
Illustration:

Array = {1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17}

Corresponding Complete Binary Tree is:
                 1
              /     \
            3         5
         /    \     /  \
        4      6   13  10
       / \    / \
      9   8  15 17

The task to build a Max-Heap from above array.

Total Nodes = 11.
Last Non-leaf node index = (N/2)-1 = (11/2) - 1 = 4.
Therefore, last non-leaf node = 6.

To build the heap, heapify only the nodes:
[1, 3, 5, 4, 6] in reverse order.

Heapify 6: Swap 6 and 17.
                 1
              /     \
            3         5
         /    \      /  \
        4      17   13  10
       / \    /  \
      9   8  15   6

Heapify 4: Swap 4 and 9.
                 1
              /     \
            3         5
         /    \      /  \
        9      17   13  10
       / \    /  \
      4   8  15   6

Heapify 5: Swap 13 and 5.
                 1
              /     \
            3         13
         /    \      /  \
        9      17   5   10
       / \    /  \
      4   8  15   6

Heapify 3: First Swap 3 and 17, again swap 3 and 15.
                 1
              /     \
            17         13
          /    \      /  \
         9      15   5   10
        / \    /  \
       4   8  3   6

Heapify 1: First Swap 1 and 17, again swap 1 and 15, 
           finally swap 1 and 6.
                 17
              /      \
            15         13
          /    \      /  \
         9      6    5   10
        / \    /  \
       4   8  3    1
```

__Questions__

1. K-th Largest Sum Contiguous Subarray
