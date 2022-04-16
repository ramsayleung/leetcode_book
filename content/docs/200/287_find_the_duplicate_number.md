+++
title = "287. Find the Duplicate Number"
author = ["Ramsay Leung"]
date = 2022-04-16T08:49:00+08:00
lastmod = 2022-04-16T08:54:49+08:00
draft = false
weight = 287
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/find-the-duplicate-number/>

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only `one repeated number` in `nums`, return this repeated number.

You must solve the problem `without` modifying the array `nums` and uses only constant extra space.

**Example 1**:

```text
Input: nums = [1,3,4,2,2]
Output: 2
```

**Example 2**:

```text
Input: nums = [3,1,3,4,2]
Output: 3
```

**Constraints**:

-   `1 <= n <= 105`
-   `nums.length == n + 1`
-   `1 <= nums[i] <= n`
-   All the integers in `nums` appear only **once** except for **precisely one integer** which appears **two or more** times.

**Follow up**:

-   How can we prove that at least one duplicate number must exist in nums?
-   Can you solve the problem in linear runtime complexity?


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
  int findDuplicate(vector<int>& nums){
    // Since each integer is in the range [1, n] inclusive, then just map the number to index
    // Time complexity: O(n)
    // Space complexity: O(1)
    while(nums[0] != nums[nums[0]]){
      std::swap(nums[0], nums[nums[0]]);
    }
    return nums[0];
  }
};
```
