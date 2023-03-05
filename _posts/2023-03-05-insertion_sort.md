---
title: Insertion Sort Algorithm
date: 2023-03-05 19:00:00 +0100
categories: [Algorithms]
tags: [algorithms, python]     # TAG names should always be lowercase
---

Given an unsorted `list` with `n` elements, the algorithm sort the values in place and return the sorted `list`.

Initial `for` statement iterate over all elements of the list, with index `i` indicating the element being sorted, where sub list `list[0:i-1]` constitute sorted elements (loop invariant), and `list[i+1:n]` the elements yet to be sorted.

At the beginning of each `for` loop iteration, the value of the element indexed by `i` is stored in variable `key`. A new index `j` is initiated pointing to prior element of `i` (value of `i - 1`).

Then the `while` statement will take `j` through all the elements down the list comparing and swapping values, until it find the one for which `list[j]` value is less than `key`. At this point, because `list[0:i-1] = sorted sublist` is loop invariant, the element being sorted found its place in the list, the `while` loop stop, and `for` continue with the next element in the list.

```python
def insertion_sort(list):
    """Sort an array with insertion sort algorithm."""
    for i in range(1, len(list)):
        key = list[i]
        j = i - 1
        while j >= 0 and list[j] > key:
            list[j + 1] = list[j]
            j -= 1
            list[j + 1] = key
    return list
```

- Time complexity = $O(n^2)$
- Space complexity = $O(1)$

# Example

The following example demonstrate steps taken by the algorithm to sort list `[4, 3, 2, 5, 1]`. At every iteration the value at index `i` is shifted to the left of the list until it find its place such that sub list `[0:i-1]` is sorted.

![Insertion sort](https://github.com/haroldgc/codingsre/blob/13111ea9f09ed47e6daeea6dbbdb2f3fbdbefc2e/img/insertion_sort.png)
