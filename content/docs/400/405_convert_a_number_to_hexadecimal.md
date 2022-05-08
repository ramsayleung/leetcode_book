+++
title = "405. Convert a Number to Hexadecimal"
author = ["Ramsay Leung"]
date = 2022-05-03T08:56:00+08:00
lastmod = 2022-05-08T08:14:40+08:00
draft = false
weight = 405
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/convert-a-number-to-hexadecimal/>

Given an integer `num`, return a string representing its hexadecimal representation. For negative integers, [two’s complement](https://en.wikipedia.org/wiki/Two%27s_complement) method is used.

All the letters in the answer string should be lowercase characters, and there should not be any leading zeros in the answer except for the zero itself.

**Note**: You are not allowed to use any built-in library method to directly solve this problem.

**Example 1**:

```text
Input: num = 26
Output: "1a"
```

**Example 2**:

```text
Input: num = -1
Output: "ffffffff"
```

**Constraints**:

-   `-2^31 <= num <= 2^31 - 1`


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <vector>
class Solution {
public:
  string toHex(int num) {
    // Space complexity: O(1)
    // Time complexity: O(N/4) => O(N)
    static std::vector<std::string> hexmap{"0", "1", "2", "3", "4", "5",
					   "6", "7", "8", "9", "a", "b",
					   "c", "d", "e", "f"};

    if (num == 0) {
      return "0";
    }

    uint32_t n = num;
    std::string result;
    while (n != 0) {
      result = hexmap[n & 15] + result;
      n = n >> 4;
    }

    return result;
  }
};
```
