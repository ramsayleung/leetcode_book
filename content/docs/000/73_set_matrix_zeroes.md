+++
title = "73. Set Matrix Zeroes"
author = ["Ramsay Leung"]
date = 2022-05-08T20:00:00+08:00
lastmod = 2022-05-08T20:11:32+08:00
draft = false
weight = 73
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/set-matrix-zeroes/>

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg" >}}

```text
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

**Example 2**:

{{< figure src="https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg" >}}

```text
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

**Constraints**:

-   `m == matrix.length`
-   `n == matrix[0].length`
-   `1 <= m, n <= 200`
-   `-2^31 <= matrix[i][j] <= 2^31 - 1`

Follow up:

-   A straightforward solution using `O(mn)` space is probably a bad idea.
-   A simple improvement uses `O(m + n)` space, but still not the best solution.
-   Could you devise a constant space solution?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <unordered_set>
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
	// Space complexity: O(m + n)
	// Time complexity: O(2 * m *n ) => O(m * n)
	int m = matrix.size();
	int n = matrix[0].size();
	std::unordered_set<int> rows;
	std::unordered_set<int> cols;
	for(int i = 0; i<m;i ++){
	    for(int j = 0; j < n; j++){
		if(matrix[i][j] == 0){
		    rows.insert(i);
		    cols.insert(j);
		}
	    }
	}

	for(int i = 0; i<m;i ++){
	    for(int j = 0; j < n; j++){
		if(cols.count(j) != 0 || rows.count(i) != 0){
		    matrix[i][j] = 0;
		}
	    }
	}
    }
};
```
