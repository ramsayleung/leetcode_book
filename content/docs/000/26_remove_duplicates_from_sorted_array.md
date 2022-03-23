+++
title = "26. Remove Duplicates from Sorted Array"
author = ["Ramsay Leung"]
date = 2022-03-19T09:02:00+08:00
lastmod = 2022-03-19T09:37:28+08:00
draft = false
weight = 26
+++

## <span class="section-num">1</span> Description {#description}

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates in-place such that each unique element appears only **once**. The relative order of the elements should be kept the **same**.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return `k` after placing the final result in the first `k` slots of `nums`.

Do **not** allocate extra space for another array. You must do this by **modifying the input array** `in-place` with O(1) extra memory.

**Custom Judge**:

The judge will test your solution with the following code:

```c++
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
  assert nums[i] == expectedNums[i];
 }
```

If all assertions pass, then your solution will be **accepted**.

Example 1:

```text
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

Example 2:

```text
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

**Constraints**:

-   `1 <= nums.length <= 3 * 10^4`
-   `-100 <= nums[i] <= 100`
-   `nums` is sorted in **non-decreasing** order.


## <span class="section-num">2</span> Soltuion {#soltuion}

Even though it works, it's not a good solution

```c++
class Solution {
public:
  int removeDuplicates(vector<int>& nums) {
    int k = 0;
    int prev = -101;
    auto iter = nums.begin();
    while(iter != nums.end()){
      if(prev == *iter){
	nums.erase(iter);
      }else{
	k++;
	prev = *iter;
	iter ++;
      }

    }

    return k;
  }
};
```
