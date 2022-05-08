+++
title = "54. Spiral Matrix"
author = ["Ramsay Leung"]
date = 2022-05-08T08:09:00+08:00
lastmod = 2022-05-08T08:13:27+08:00
draft = false
weight = 54
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/spiral-matrix/>

Given an `m x n` `matrix`, return all elements of the `matrix` in spiral order.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg" >}}

```text
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2**:

{{< figure src="https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg" >}}

```text
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

**Constraints**:

-   `m == matrix.length`
-   `n == matrix[i].length`
-   `1 <= m, n <= 10`
-   `-100 <= matrix[i][j] <= 100`


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <iostream>
class Solution {
public:
  vector<int> spiralOrder(vector<vector<int>>& matrix) {
    // Time complexity: O(m * n)
    // Space complexity: O(m * n)

    int m = matrix.size();
    int n = matrix[0].size();
    int left = 0, right = n -1;
    int up  = 0, down = m - 1;
    int j = 0;
    std::vector<int> result;
    result.reserve(m * n); // this single statement makes this solution faster than 100.00% of C++ online submissions

    while(j < m * n){
      for(int i = left; i <= right && j < m *n; i++, j++){
	result.push_back(matrix[up][i]);
      }

      for(int i = up + 1; i<= down && j < m* n; i++, j++){
	result.push_back(matrix[i][right]);
      }

      for(int i = right - 1; i>=left && j < m * n; i--, j++){
	result.push_back(matrix[down][i]);
      }

      for(int i = down - 1; i > up && j < m*n; i--, j++){
	result.push_back(matrix[i][left]);
      }

      left++, right--, up++, down--;
    }
    return result;
  }
};
```
