+++
title = "88. Merge Sorted Array"
author = ["Ramsay Leung"]
date = 2022-04-29T23:41:00+08:00
lastmod = 2022-05-08T08:17:23+08:00
draft = false
weight = 88
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/merge-sorted-array/>
You are given two integer arrays `nums1` and `nums2`, sorted in `non-decreasing order`, and two integers m and n, representing the number of elements in `nums1` and `nums2` respectively.

**Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing** order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first m elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

**Example 1**:

```text
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```

**Example 2**:

```text
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
```

**Example 3**:

```text
Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
```

**Constraints**:

-   `nums1.length == m + n`
-   `nums2.length == n`
-   `0 <= m, n <= 200`
-   `1 <= m + n <= 200`
-   `-10^9 <= nums1[i], nums2[j] <= 10^9`

Follow up: Can you come up with an algorithm that runs in O(m + n) time?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <algorithm>
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
	// Space complexity: O(1)
	// Time complexity: O(2N + M)
	std::copy(nums2.begin(), nums2.end(), nums1.begin() + m);
	std::inplace_merge(nums1.begin(), nums1.begin() +m, nums1.end());
    }
};
```
