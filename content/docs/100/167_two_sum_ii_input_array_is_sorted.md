+++
title = "167. Two Sum II - Input Array Is Sorted"
author = ["Ramsay Leung"]
date = 2022-05-03T09:01:00+08:00
lastmod = 2022-05-08T08:14:31+08:00
draft = false
weight = 167
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/>

Given a **1-indexed** array of integers `numbers` that is already sorted in **non-decreasing order**, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, **added by one** as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

**Example 1**:

```text
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

**Example 2**:

```text
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].
```

**Example 3**:

```text
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].
```

**Constraints**:

-   `2 <= numbers.length <= 3 * 10^4`
-   `-1000 <= numbers[i] <= 1000`
-   numbers is sorted in **non-decreasing order**.
-   `-1000 <= target <= 1000`
-   The tests are generated such that there is exactly **one solution**.


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <algorithm>
class Solution {
public:
  vector<int> twoSum(vector<int>& numbers, int target) {
    // Space complexity: O(1)
    // Time complexity: O(N)
    int low = 0;
    int high = numbers.size() - 1;
    while(numbers[low] + numbers[high] != target){
      if(numbers[low] + numbers[high] < target){
	low ++;
      }else{
	high--;
      }
    }

    std::vector<int> result{low + 1, high + 1};
    return result;
  }
};
```
