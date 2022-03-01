+++
title = "67. Add Binary"
author = ["Ramsay Leung"]
date = 2022-03-01T21:03:00+08:00
lastmod = 2022-03-01T21:33:06+08:00
draft = false
weight = 67
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/add-binary/>
Given two binary strings `a` and `b`, return their sum as a binary string.

Example 1:

```text
Input: a = "11", b = "1"
Output: "100"
```

Example 2:

```text
Input: a = "1010", b = "1011"
Output: "10101"
```

**Constraints**:

-   `1 <= a.length, b.length <= 10^4`
-   `a` and `b` consist only of `'0'` or `'1'` characters.
-   Each string does not contain leading zeros except for the zero itself.


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/67_add_binary.png" link="/ox-hugo/67_add_binary.png" >}}

```c++
class Solution {
public:
  string addBinary(string a, string b) {
    // runtime complexity: O(N), N = max(a.size(), b.size());
    // space complexity: O(N), N = max(a.size(), b.size());
    auto p_a = a.c_str();
    auto p_b = b.c_str();
    auto sizea = a.size();
    auto sizeb = b.size();
    std::string result = (sizea > sizeb ? a : b);
    int i = 0, j = 0, k = 0;
    int carry = 0;

    for (i = sizea - 1, j = sizeb - 1, k = result.size() - 1; i >= 0 || j >= 0;
	 i--, j--, k--) {
      int add_result = 0;
      if (i >= 0) {
	add_result += p_a[i] - '0';
      }
      if (j >= 0) {
	add_result += p_b[j] - '0';
      }

      add_result += carry;
      if (add_result % 2 == add_result) {
	result[k] = add_result + '0';
	carry = 0;
      } else {
	result[k] = add_result % 2 + '0';
	carry = 1;
      }
    }

    if (carry != 0) {
      result = '1' + result;
    }
    return result;
  }
};
```
