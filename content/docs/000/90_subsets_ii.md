+++
title = "90. Subsets II"
author = ["Ramsay Leung"]
date = 2022-05-12T22:50:00+08:00
lastmod = 2022-05-12T22:54:15+08:00
draft = false
weight = 90
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/subsets-ii/>

Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set).

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1**:

```text
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

**Example 2**:

```text
Input: nums = [0]
Output: [[],[0]]
```

**Constraints**:

-   `1 <= nums.length <= 10`
-   `-10 <= nums[i] <= 10`


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <algorithm>
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
	// Time complexity: O(N!), N is the size of nums
	// Space complexity: O(N!)
	std::vector<std::vector<int>> result;
	std::vector<int> path;
	std::sort(nums.begin(), nums.end());
	backtrack(nums, 0, result, path);
	return result;
    }
private:
    void backtrack(const std::vector<int>& nums, int start, std::vector<std::vector<int>>& result, std::vector<int>& path){
	result.push_back(path);
	for(int i = start; i < nums.size(); i++){
	    // skip duplicate
	    if(i > start && nums[i] == nums[i - 1]){
		continue;
	    }
	    path.push_back(nums[i]);
	    backtrack(nums, i + 1, result, path);
	    path.pop_back();
	}
    }
};
```
