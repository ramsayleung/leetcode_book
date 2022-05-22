+++
title = "216. Combination Sum III"
author = ["Ramsay Leung"]
date = 2022-05-12T22:10:00+08:00
lastmod = 2022-05-12T22:14:57+08:00
draft = false
weight = 216
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/combination-sum-iii/>

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

Only numbers `1` through `9` are used.
Each number is used at `most once`.
Return a list of all possible valid combinations. The list must not contain the same combination twice, and the combinations may be returned in any order.

**Example 1**:

```text
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```

**Example 2**:

```text
Input: k = 3, n = 9
Output: [[1,2,6],[1,3,5],[2,3,4]]
Explanation:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.
```

**Example 3**:

```text
Input: k = 4, n = 1
Output: []
Explanation: There are no valid combinations.
Using 4 different numbers in the range [1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.
```

**Constraints**:

-   `2 <= k <= 9`
-   `1 <= n <= 60`


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
  vector<vector<int>> combinationSum3(int k, int n) {
    // Time complexity: (10 - 1) * (10 -2) * .. * (10 -k)
    // Space complexity:
    // faster than 100.00% of C++ online submissions for Combination Sum III.
    std::vector<std::vector<int>> result;
    std::vector<int> path;
    backtrack(k, n, 1, result, path);
    return result;
  }
private:
  void backtrack(int k, int target, int start, std::vector<std::vector<int>>& result, std::vector<int>& path){
    if(k < 0 || target < 0){
      return;
    }

    if (k == 0 && target == 0){
      result.push_back(path);
    }

    for(int i = start; i < 10; i++){
      path.push_back(i);
      backtrack(k - 1, target - i, i + 1, result, path);
      path.pop_back();
    }
  }
};
```
