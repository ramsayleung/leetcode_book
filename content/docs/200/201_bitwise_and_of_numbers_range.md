+++
title = "201. Bitwise AND of Numbers Range"
author = ["Ramsay Leung"]
date = 2022-05-01T13:54:00+08:00
lastmod = 2022-05-08T08:14:55+08:00
draft = false
weight = 201
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/bitwise-and-of-numbers-range/>

Given two integers `left` and `right` that represent the range `[left, right]`, return the bitwise AND of all numbers in this range, inclusive.

**Example 1**:

```text
Input: left = 5, right = 7
Output: 4
```

**Example 2**:

```text
Input: left = 0, right = 0
Output: 0
```

**Example 3**:

```text
Input: left = 1, right = 2147483647
Output: 0
```

**Constraints**:

-   `0 <= left <= right <= 2^31 - 1`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/201-bitwise-and-of-numbers-range.png" link="/ox-hugo/201-bitwise-and-of-numbers-range.png" >}}

```C++
#include <limits>
class Solution {
public:
  int rangeBitwiseAnd(int left, int right) {
    // Time complexity: O(32) => O(1)
    // Space complexity: O(1)
    if(left == 0){
      return 0;
    }

    int diff_bit_count = 0;
    while(left != right){
      left = left >> 1;
      right = right >> 1;
      diff_bit_count++;
    }

    return right << diff_bit_count;
  }
};
```
