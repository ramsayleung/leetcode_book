+++
title = "34. Find First and Last Position of Element in Sorted Array"
author = ["Ramsay Leung"]
date = 2020-04-27T16:05:11
lastmod = 2022-04-16T21:09:08+08:00
draft = false
weight = 34
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/>

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return `[-1, -1]`.

**Example 1**:

```text

Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

```

**Example 2**:

```text
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```


## <span class="section-num">2</span> Solution {#solution}

```python
# Runtime: 80 ms, faster than 95.74% of Python3 online submissions for Find First and Last Position of Element in Sorted Array.
# time complexity: O(2*logn)->O(logn), 2 is because we search twice.
# space complexity: O(1)
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
	if len(nums) == 0:
	    return [-1,-1]
	# 找出最左边等于target的元素的位置
	binarySearchLeft = lambda x,y: x<y
	# 找出最左边大于target的元素的位置 x, 若 nums[x] 刚大于target, 那么
	# nums[x-1] 就是最右边等于target的元素.
	binarySearchRight = lambda x,y: x<=y
	def binarySearch(condition)->int:
	    low = 0
	    high = len(nums)
	    while low < high:
		mid = (low+high) // 2
		if condition(nums[mid],target):
		    low = mid + 1
		else:
		    high = mid
	    return low
	first = binarySearch(binarySearchLeft)
	last = binarySearch(binarySearchRight) - 1
	return [first, last] if first<len(nums) and nums[first] == target else [-1,-1]
```

```C++
#include <algorithm>
class Solution {
public:
  vector<int> searchRange(vector<int>& nums, int target) {
    // Space complexity: O(1)
    // Time complexity: O(2 logN) => O(logN)
    if(0 == nums.size()){
      std::vector<int> result{-1, -1};
      return result;
    }

    auto low = std::lower_bound(nums.begin(), nums.end(), target);
    if(low == nums.end() || *low != target){
      std::vector<int> result{-1, -1};
      return result;
    }

    auto high = std::upper_bound(low, nums.end(), target);
    std::vector<int> result{static_cast<int>(low - nums.begin()), static_cast<int>(high - nums.begin() - 1)};
    return result;
  }
};
```
