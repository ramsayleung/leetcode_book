+++
title = "171. Excel Sheet Column Number"
author = ["Ramsay Leung"]
date = 2022-05-21T17:44:00+08:00
lastmod = 2022-05-21T17:49:31+08:00
draft = false
weight = 171
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/excel-sheet-column-number/>

Given a string `columnTitle` that represents the column title as appears in an Excel sheet, return its corresponding column number.

For example:

```text
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28
...
```

**Example 1**:

```text
Input: columnTitle = "A"
Output: 1
```

**Example 2**:

```text
Input: columnTitle = "AB"
Output: 28
```

**Example 3**:

```text
Input: columnTitle = "ZY"
Output: 701
```

**Constraints**:

-   `1 <= columnTitle.length <= 7`
-   `columnTitle` consists only of uppercase English letters.
-   `columnTitle` is in the range `["A", "FXSHRXW"]`.


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
  int titleToNumber(string columnTitle) {
    // Time complexity: O(N), N is the size of columnTitle
    // Space complexity: O(1)
    int size = columnTitle.size();
    long result = 0;
    for(int i = 0; i < size; i++){
      result = result * 26 + columnTitle[i] - 'A' + 1;
    }
    return result;
  }
};
```
