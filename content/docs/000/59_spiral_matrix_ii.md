+++
title = "59. Spiral Matrix II"
author = ["Ramsay Leung"]
date = 2022-05-08T08:49:00+08:00
lastmod = 2022-05-08T08:52:36+08:00
draft = false
weight = 59
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/spiral-matrix-ii/>
Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n^2` in spiral order.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg" >}}

```text
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

**Example 2**:

```text
Input: n = 1
Output: [[1]]
```

**Constraints**:

-   `1 <= n <= 20`


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:

    vector<vector<int>> generateMatrix(int n) {
	// Space complexity: O(n * n)
	// Time complexity: O(n * n)
	// faster than 100.00% of C++ online submissions for Spiral Matrix II

	std::vector<std::vector<int>> result;
	result.reserve(n);
	for(int i = 0; i< n; i++){
	    std::vector<int> init(n, 0);
	    result.push_back(init);
	}

	int up = 0, down = n - 1, left = 0, right = n - 1;
	int j = 0;

	while(j < n * n){
	    for(int i = left; i <= right && j < n*n; i++){
		result[up][i] = ++j;
	    }

	    for(int i = up + 1; i <= down && j < n *n; i++){
		result[i][right] = ++j;
	    }

	    for(int i = right - 1; i >= left && j < n * n; i--){
		result[down][i] = ++j;
	    }

	    for(int i = down - 1; i > up && j < n * n; i--){
		result[i][left] = ++j;
	    }

	    left++, right--, up++, down--;
	}

	return result;
    }
};
```
