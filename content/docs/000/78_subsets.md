+++
title = "78. Subsets"
author = ["Ramsay Leung"]
date = 2020-04-26T22:15:08
lastmod = 2022-05-12T22:10:02+08:00
draft = false
weight = 78
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/subsets/>

Given a set of **distinct** integers, nums, return all possible subsets (the power set).

**Note**: The solution set must not contain duplicate subsets.

**Example**:

```text
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```


## <span class="section-num">2</span> Solution {#solution}

```python
from typing import List
# Runtime: 32 ms, faster than 73.24% of Python3 online submissions for Subsets.
# time complexity: O(N*2^N) to generate all subsets and then copy them into
# output list
# space complexity: O(2^N) 2^N subsets for the length, every subset need O(N) to store
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
	output: List[List[int]] = []
	seen = set()
	length = len(nums)
	def backtracking(start: int, subset: List[int]) ->None:
	    if start >= length:
		output.append(subset.copy())
		return
	    for idx in range(start, length):
		if tuple(subset) not in seen:
		    seen.add(tuple(subset))
		    output.append(subset)
		if nums[idx] not in set(subset):
		    backtracking(idx+1, subset+[nums[idx]])
	backtracking(0, [])
	return output
```

```C++
class Solution {
public:
  vector<vector<int>> subsets(vector<int>& nums) {
    // faster than 100.00% of C++ online submissions for Subsets.
    // Time complexity: O(N!) N is the size of nums.
    // Space complexity: O(N!)
    std::vector<std::vector<int>> result;
    std::vector<int> path;
    backtrack(nums, 0, result, path);
    return result;
  }
private:
  void backtrack(const std::vector<int>& nums, int start, std::vector<std::vector<int>>& result, std::vector<int>& path){
    result.push_back(path);
    for(int i = start; i < nums.size(); i++){
      path.push_back(nums[i]);
      backtrack(nums, i + 1, result, path);
      path.pop_back();
    }
  }
};
```
