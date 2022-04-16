+++
title = "162. Find Peak Element"
author = ["Ramsay Leung"]
date = 2022-04-16T09:02:00+08:00
lastmod = 2022-04-16T09:11:30+08:00
draft = false
weight = 162
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/find-peak-element/>

A peak element is an element that is strictly greater than its neighbors.

Given an integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`.

You must write an algorithm that runs in `O(log n)` time.

**Example 1**:

```text
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2**:

```text
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```

**Constraints**:

-   `1 <= nums.length <= 1000`
-   `-2^31 <= nums[i] <= 2^31 - 1`
-   `nums[i] != nums[i + 1]` for all valid `i`.


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
  int findPeakElement(vector<int> &nums) {
    // Time complexity: O(logN)
    // Space complexity: O(1)
    int low = 0;
    int high = nums.size();
    int mid = 0;
    while (low <= high) {
      mid = (low + high) / 2;
      if (mid != 0 && nums[mid] < nums[mid - 1]) {
	high = mid - 1;
      } else if (mid != nums.size() - 1 && nums[mid] < nums[mid + 1]) {
	low = mid + 1;
      } else {
	return mid;
      }
    }

    return mid;
  }
};
```
