+++
title = "434. Number of Segments in a String"
author = ["Ramsay Leung"]
date = 2022-05-21T17:53:00+08:00
lastmod = 2022-05-21T18:01:44+08:00
draft = false
weight = 434
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/number-of-segments-in-a-string/>

Given a string s, return the number of segments in the string.

A segment is defined to be a contiguous sequence of non-space characters.

**Example 1**:

```text
Input: s = "Hello, my name is John"
Output: 5
Explanation: The five segments are ["Hello,", "my", "name", "is", "John"]
```

**Example 2**:

```text
Input: s = "Hello"
Output: 1
```

**Constraints**:

-   `0 <= s.length <= 300`
-   `s` consists of lowercase and uppercase English letters, digits, or one of the following characters `"!@#$%^&*()_+-=',.:"`.
-   The only space character in `s` is `' '`.


## <span class="section-num">2</span> Solution {#solution}
