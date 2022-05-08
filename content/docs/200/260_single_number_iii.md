+++
title = "260. Single Number III"
author = ["Ramsay Leung"]
date = 2022-05-01T11:18:00+08:00
lastmod = 2022-05-08T08:15:13+08:00
draft = false
weight = 260
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/single-number-iii/>
Given an integer array `nums`, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in **any order**.

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.

**Example 1**:

```text
Input: nums = [1,2,1,3,2,5]
Output: [3,5]
Explanation:  [5, 3] is also a valid answer.
```

**Example 2**:

```text
Input: nums = [-1,0]
Output: [-1,0]
Example 3:

Input: nums = [0,1]
Output: [1,0]
```

**Constraints**:

-   `2 <= nums.length <= 3 * 10^4`
-   `-2^31 <= nums[i] <= 2^31 - 1`
-   Each integer in nums will appear twice, only two integers will appear once.


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/260-single-number-iii.png" link="/ox-hugo/260-single-number-iii.png" >}}

```C++
#include <numeric>
#include <limits>
#include <functional>
class Solution {
public:
  vector<int> singleNumber(vector<int>& nums) {
    // Time complexity: O(2N) => O(N)
    // Space complexity: O(1)
    int diff = std::accumulate(nums.begin(), nums.end(), 0, std::bit_xor<>{});
    // find the last set bit
    // corner case
    if(diff == std::numeric_limits<int>::min()){
      diff = 0;
    }else{
      diff &= (~diff + 1);
    }

    std::vector<int> result{0, 0};
    for(const auto& num: nums){
      if(diff&num){
	result[0]^= num;
      }else{
	result[1]^=num;
      }
    }
    return result;
  }
};
```
