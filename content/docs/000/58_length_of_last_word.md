+++
title = "58. Length of Last Word"
author = ["Ramsay Leung"]
date = 2022-05-18T22:20:00+08:00
lastmod = 2022-05-18T22:28:26+08:00
draft = false
weight = 58
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/length-of-last-word/>

Given a string `s` consisting of some words separated by some number of spaces, return the length of the **last** word in the string.

A **word** is a maximal substring consisting of non-space characters only.

**Example 1**:

```text
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

**Example 2**:

```text
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```

**Example 3**:

```text
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

**Constraints**:

-   `1 <= s.length <= 10^4`
-   `s` consists of only English letters and spaces `' '`.
-   There will be at least one word in `s`.


## <span class="section-num">2</span> Solution {#solution}

```C++
class Solution {
public:
    int lengthOfLastWord(string s) {
	// Time complexity: O(N), N is the size of s
	// Space complexity: O(1)
	// faster than 100.00% of C++
	int last_index = s.size() - 1;
	while(last_index >= 0 && s[last_index] == ' '){
	    last_index--;
	}

	int length = 0;
	while(last_index >=0 && s[last_index] != ' '){
	    length ++;
	    last_index --;
	}

	return length;
    }
};
```
