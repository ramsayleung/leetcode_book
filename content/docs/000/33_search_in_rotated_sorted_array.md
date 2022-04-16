+++
title = "33. Search in Rotated Sorted Array"
author = ["Ramsay Leung"]
date = 2022-04-16T08:57:00+08:00
lastmod = 2022-04-16T09:01:48+08:00
draft = false
weight = 33
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/search-in-rotated-sorted-array/>

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, nums is **possibly rotated** at an unknown pivot index k (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` after the possible rotation and an `integer`, return the index of `target` if it is in `nums`, or `-1` if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1**:

```text
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2**:

```text
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

**Example 3**:

```text
Input: nums = [1], target = 0
Output: -1
```

**Constraints**:

-   `1 <= nums.length <= 5000`
-   `-10^4 <= nums[i] <= 10^4`
-   All values of nums are **unique**.
-   `nums` is an ascending array that is possibly rotated.
-   `-10^4 <= target <= 10^4`


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
	int low = 0;
	int high = nums.size() - 1;
	while(low <= high){
	    int mid = (low + high) / 2;
	    if(nums[mid] == target){
		return mid;
	    }

	    // the left half is sorted
	    if(nums[mid] >= nums[low]){
		if(target <= nums[mid] && nums[low] <= target ){
		    high = mid - 1;
		}else{
		    low = mid + 1;
		}
	    }else{
		if(target <= nums[high] && nums[mid] <= target){
		    low = mid + 1;
		}else{
		    high = mid - 1;
		}
	    }
	}

	return -1;
    }
};
```
