+++
title = "378. Kth Smallest Element in a Sorted Matrix"
author = ["Ramsay Leung"]
date = 2022-04-29T22:55:00+08:00
lastmod = 2022-05-08T08:19:23+08:00
draft = false
weight = 378
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/>

Given an `n x n` matrix where each of the rows and columns is sorted in ascending order, return the `k^th` smallest element in the matrix.

Note that it is the `k^th` smallest element in the **sorted order**, not the `k^th` **distinct** element.

You must find a solution with a memory complexity better than O(n^2).

**Example 1**:

```text
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8th smallest number is 13
```

**Example 2**:

```text
Input: matrix = [[-5]], k = 1
Output: -5
```

**Constraints**:

-   `n == matrix.length == matrix[i].length`
-   `1 <= n <= 300`
-   `-10^9 <= matrix[i][j] <= 10^9`
-   All the rows and columns of `matrix` are **guaranteed** to be sorted in **non-decreasing order**.
-   `1 <= k <= n^2`

**Follow up**:

-   Could you solve the problem with a constant memory (i.e., `O(1)` memory complexity)?
-   Could you solve the problem in `O(n)` time complexity? The solution may be too advanced for an interview but you may find reading this paper fun.


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <algorithm>
#include <cmath>
class Solution {
public:
  int kthSmallest(vector<vector<int>> &matrix, int k) {
    // Time complexity: O(m * n * LogK)
    // Space complexity: O(k)
    std::vector<int> result;
    std::make_heap(result.begin(), result.end());
    int size = matrix.size();
    for (int i = 0; i < size; i++) {
      for (int j = 0; j < size; j++) {
	result.push_back(matrix[i][j]);
	std::push_heap(result.begin(), result.end());
	if (result.size() > k) {
	  std::pop_heap(result.begin(), result.end());
	  result.pop_back();
	}
      }
    }

    std::pop_heap(result.begin(), result.end());
    return result.back();
  }
};
```
