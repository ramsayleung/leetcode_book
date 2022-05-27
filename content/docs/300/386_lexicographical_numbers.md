+++
title = "386. Lexicographical Numbers"
author = ["Ramsay Leung"]
date = 2022-05-27T20:51:00+08:00
lastmod = 2022-05-27T20:55:58+08:00
draft = false
weight = 386
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/lexicographical-numbers/>

Given an integer `n`, return all the numbers in the range `[1, n]` sorted in lexicographical order.

You must write an algorithm that runs in `O(n)` time and uses `O(1)` extra space.

**Example 1**:

```text
Input: n = 13
Output: [1,10,11,12,13,2,3,4,5,6,7,8,9]
```

**Example 2**:

```text
Input: n = 2
Output: [1,2]
```

**Constraints**:

-   `1 <= n <= 5 * 10^4`


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <vector>
class Solution {
public:
  vector<int> lexicalOrder(int n) {
    // Time complexity: O(N)
    // space complexity: O(1)
    int upper = std::min(9, n);
    std::vector<int> result;

    for (int i = 1; i <= upper; i++) {
      dfs(i, n, result);
    }
    return result;
  }

  void dfs(int val, int n, std::vector<int> &result) {
    if (val <= n) {
      result.push_back(val);
      for (int i = 0; i <= 9; i++) {
	if (val * 10 + i <= n) {
	  dfs(val * 10 + i, n, result);
	}
      }
    }
  }
};
```
