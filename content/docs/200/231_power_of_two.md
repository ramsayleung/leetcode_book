+++
title = "231. Power of Two"
author = ["Ramsay Leung"]
date = 2022-04-10T21:12:00+08:00
lastmod = 2022-04-17T15:34:51+08:00
draft = false
weight = 231
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/power-of-two/>

Given an integer `n`, return `true` if it is a power of two. Otherwise, return `false`.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2^x`.

**Example 1**:

```text
Input: n = 1
Output: true
Explanation: 20 = 1
```

**Example 2**:

```text
Input: n = 16
Output: true
Explanation: 24 = 16
```

**Example 3**:

```text
Input: n = 3
Output: false
```

**Constraints**:

-   `-2^31 <= n <= 2^31 - 1`

**Follow up**: Could you solve it without loops/recursion?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <bitset>
class Solution {
public:
  bool isPowerOfTwo(int n) {
    // Space complexity: O(33) => O(1)
    // Time complexity: O(1)
    return std::bitset<33>(n).count() == 1;
  }
};
```
