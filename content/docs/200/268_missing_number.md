+++
title = "268. Missing Number"
author = ["Ramsay Leung"]
date = 2022-04-10T14:17:00+08:00
lastmod = 2022-04-11T22:28:34+08:00
draft = false
weight = 268
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/missing-number/>

Given an array `nums` containing n distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

**Example 1**:

```text
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
```

**Example 2**:

```text
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
```

**Example 3**:

```text
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
```

**Constraints**:

-   `n == nums.length`
-   `1 <= n <= 10^4`
-   `0 <= nums[i] <= n`
-   All the numbers of `nums` are **unique**.

**Follow up**: Could you implement a solution using only `O(1)` extra space complexity and `O(n)` runtime complexity?


## <span class="section-num">2</span> Solution {#solution}

```c++
#include <vector>
class Solution {
public:
  int missingNumber(vector<int>& nums) {
    // Time complexity: O(n), n is the size of nums.
    // Space complexity: O(1)
    int n = nums.size();
    int expected_sum = n * (n + 1) / 2.0;
    for(const auto& num: nums){
      expected_sum -= num;
    }
    return expected_sum;
  }
};
```
