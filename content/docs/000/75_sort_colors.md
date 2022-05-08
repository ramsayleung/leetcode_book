+++
title = "75. Sort Colors"
author = ["Ramsay Leung"]
date = 2022-04-30T08:54:00+08:00
lastmod = 2022-05-08T08:16:05+08:00
draft = false
weight = 75
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/sort-colors/>

Given an array `nums` with `n` objects colored red, white, or blue, sort them [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1**:

```text
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

**Example 2**:

```text
Input: nums = [2,0,1]
Output: [0,1,2]
```

**Constraints**:

-   `n == nums.length`
-   `1 <= n <= 300`
-   `nums[i]` is either `0`, `1`, or `2`.

**Follow up**: Could you come up with a one-pass algorithm using only constant extra space?


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
  void sortColors(vector<int>& nums) {
    // Time complexity: O(2N) => O(N), N is the size of nums
    // Space complexity: O(1)
    int red_cnt = 0;
    int white_cnt = 0;
    int blue_cnt = 0;
    for(const auto& color: nums){
      if(0 == color){
	red_cnt++;
      }else if(1 == color){
	white_cnt ++;
      }else{
	blue_cnt ++;
      }
    }

    for(int i = 0; i<nums.size(); i++){
      if(red_cnt-- >0){
	nums[i] = 0;
      }else if(white_cnt-- >0){
	nums[i] = 1;
      }else{
	nums[i] = 2;
	blue_cnt --;
      }
    }
  }
};
```
