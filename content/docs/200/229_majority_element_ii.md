+++
title = "229. Majority Element II"
author = ["Ramsay Leung"]
date = 2022-04-10T13:07:00+08:00
lastmod = 2022-04-11T22:27:04+08:00
draft = false
weight = 229
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/majority-element-ii/>

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1**:

```text
Input: nums = [3,2,3]
Output: [3]
```

**Example 2**:

```text
Input: nums = [1]
Output: [1]
```

**Example 3**:

```text
Input: nums = [1,2]
Output: [1,2]
```

**Constraints**:

-   `1 <= nums.length <= 5 * 10^4`
-   `-10^9 <= nums[i] <= 10^9`

**Follow up**: Could you solve the problem in linear time and in `O(1)` space?


## <span class="section-num">2</span> Solution {#solution}

```c++
#include <unordered_map>
#include <vector>
class Solution {
public:
  vector<int> majorityElement(vector<int> &nums) {
    // Runtime complexity: O(n). n is the size of nums.
    // Space complexity: O(n).
    std::vector<int> result;
    if (nums.size() == 0) {
      return result;
    }

    std::unordered_map<int, int> occur;
    int threshold = nums.size() / 3;
    for (const auto &num : nums) {
      auto iter = occur.find(num);
      if (iter != occur.end()) {
	iter->second++;
      } else {
	occur[num] = 1;
      }

      if (occur[num] > threshold) {
	result.emplace_back(num);
	// since num has been added into result, just making it impossible to be
	// added twice.
	occur[num] = -0x709394;
      }
    }

    return result;
  }
};
```
