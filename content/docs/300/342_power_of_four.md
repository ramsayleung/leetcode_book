+++
title = "342. Power of Four"
author = ["Ramsay Leung"]
date = 2022-04-14T22:57:00+08:00
lastmod = 2022-04-17T15:34:48+08:00
draft = false
weight = 342
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/power-of-four/>

Given an integer `n`, return `true` if it is a power of four. Otherwise, return `false`.

An integer `n` is a power of four, if there exists an integer `x` such that `n == 4^x`.

**Example 1**:

```text
Input: n = 16
Output: true
```

**Example 2**:

```text
Input: n = 5
Output: false
```

**Example 3**:

```text
Input: n = 1
Output: true
```

**Constraints**:

`-2^31 <= n <= 2^31 - 1`

**Follow up**: Could you solve it without loops/recursion?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <bitset>
class Solution {
public:
  bool isPowerOfFour(int n) {
    // Space complexity: O(33) -> O(1)
    // Time complexity: O(33) -> O(1)
    std::bitset<33> binary = std::bitset<33>(n);
    if (binary.count() != 1) {
      return false;
    }

    std::string bin_str = binary.to_string();
    for (int i = bin_str.size() - 1; i >= 0; i--) {
      if (bin_str[i] == '1') {
	return (bin_str.size() - 1 - i) % 2 == 0;
      }
    }

    return false;
  }
};
```
